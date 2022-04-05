---
title: SwiftUI MainActor Wrapper
---

### Main Idea
 @MainActor is a global actor that uses the main queue for executing its work. In practice, this means methods or types marked with @MainActor can (for the most part) safely modify the UI because it will always be running on the main queue, and calling MainActor.run() will push some custom work of your choosing to the main actor, and thus to the main queue. At the simplest level both of these features are straightforward to use, but as you’ll see there’s a lot of complexity behind them.
 
 The magic of @MainActor is that it automatically forces methods or whole types to run on the main actor, a lot of the time without any further work from us. Previously we needed to do it by hand, remembering to use code like DispatchQueue.main.async() or similar every place it was needed, but now the compiler does it for us automatically.

```swift
@MainActor
class AccountViewModel: ObservableObject {
    @Published var username = "Anonymous"
    @Published var isAuthenticated = false
}

```

Be careful: @MainActor is really helpful to make code run on the main actor, but it’s not foolproof. For example, if you have a @MainActor class then in theory all its methods will run on the main actor, but one of those methods could trigger code to run on a background task. For example, if you’re using Face ID and call evaluatePolicy() to authenticate the user, the completion handler will be called on a background thread even though that code is still within the @MainActor class.

If you do need to spontaneously run some code on the main actor, you can do that by calling MainActor.run() and providing your work. This allows you to safely push work onto the main actor no matter where your code is currently running, like this:

```swift
func couldBeAnywhere() async {
    await MainActor.run {
        print("This is on the main actor.")
    }
}

await couldBeAnywhere()
```

You can send back nothing from run() if you want, or send back a value like this:

```swift
func couldBeAnywhere() async {
    let result = await MainActor.run { () -> Int in
        print("This is on the main actor.")
        return 42
    }

    print(result)
}

await couldBeAnywhere()
```

If you wanted the work to be sent off to the main actor without waiting for its result to come back, you can place it in a new task like this:
```swift 
func couldBeAnywhere() {
    Task {
        await MainActor.run {
            print("This is on the main actor.")
        }
    }

    // more work you want to do
}

couldBeAnywhere()

func couldBeAnywhere() {
    Task { @MainActor in
        print("This is on the main actor.")
    }

    // more work you want to do
}

couldBeAnywhere()
```
Important: If your function is already running on the main actor, using await MainActor.run() will run your code immediately without waiting for the next run loop, but using Task as shown above will wait for the next run loop.

```swift
@MainActor class ViewModel: ObservableObject {
    func runTest() async {
        print("1")

        await MainActor.run {
            print("2")

            Task { @MainActor in
                print("3")
            }

            print("4")
        }

        print("5")
    }
}
```
