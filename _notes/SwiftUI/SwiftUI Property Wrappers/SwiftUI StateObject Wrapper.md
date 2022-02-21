---
title: SwiftUI StateObject Wrapper
---

### Main Idea

If you want to use a class with your SwiftUI data – which you will want to do if that data should be shared across more than one view – then SwiftUI gives us three property wrappers that are useful: @StateObject, @ObservedObject, and @EnvironmentObject.

@Published is more or less half of @State: it tells Swift that whenever either of those two properties changes, it should send an announcement out to any SwiftUI views that are watching that they should reload.

How do those views know which classes might send out these notifications? That’s another property wrapper, @StateObject, which is the other half of @State – it tells SwiftUI that we’re creating a new class instance that should be watched for any change announcements.

When you want to use a class instance elsewhere – when you’ve created it in view A using @StateObject and want to use that same object in view B – you use a slightly different property wrapper called @ObservedObject. That’s the only difference: when creating the shared data use @StateObject, but when you’re just using it in a different view you should use @ObservedObject instead.
### Usage

```swift
// Make a class that conforms to the ObservableObject protocol.
class User: ObservableObject {
    // Mark some properties with @Published so that any views using the class get updated when they change.
    @Published var firstName = "Bilbo"
    @Published var lastName = "Baggins"
}

struct ContentView: View {
    // Create an instance of our class using the @StateObject property wrapper.
    @StateObject var user = User()
    
    var body: some View {
        VStack {
            Text("Your name is \(user.firstName) \(user.lastName)")
            
            TextField("First Name", text: $user.firstName)
            TextField("Last Name", text: $user.lastName)
        }
    }
}
```
