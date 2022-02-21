---
title: Swift UserDefaults
---

### Main Idea

One common way to store a small amount of data is called UserDefaults, and it’s great for simple user preferences. There is no specific number attached to “a small amount”, but everything you store in UserDefaults will automatically be loaded when your app launches – if you store a lot in there your app launch will slow down. To give you at least an idea, you should aim to store no more than 512KB in there.

UserDefaults is perfect for storing things like when the user last launched the app, which news story they last read, or other passively collected information. Even better, SwiftUI can often wrap up UserDefaults inside a nice and simple property wrapper called @AppStorage – it only supports a subset of functionality right now, but it can be really helpful.

Now, I mentioned that SwiftUI provides an @AppStorage property wrapper around UserDefaults, and in simple situations like this one it’s really helpful. What it does is let us effectively ignore UserDefaults entirely, and just use @AppStorage rather than @State, like this:

Clearly using @AppStorage is easier than UserDefaults: it’s one line of code rather than two, and it also means we don’t have to repeat the key name each time. However, right now at least @AppStorage doesn’t make it easy to handle storing complex objects such as Swift structs – perhaps because Apple wants us to remember that storing lots of data in there is a bad idea!

```swift
struct ContentView: View {
    @State private var tapCount = UserDefaults.standard.integer(forKey: "Tap")
        
    var body: some View {
        Button("Tap Count: \(tapCount)") {
            tapCount += 1
            // We need to use UserDefaults.standard. This is the built-in instance of UserDefaults that is attached to our app, but in more advanced apps you can create your own instances. For example, if you want to share defaults across several app extensions you might create your own UserDefaults instance.
            // There is a single set() method that accepts any kind of data – integers, Booleans, strings, and more.
            // We attach a string name to this data, in our case it’s the key “Tap”. This key is case-sensitive, just like regular Swift strings, and it’s important – we need to use the same key to read the data back out of UserDefaults.
            UserDefaults.standard.set(self.tapCount, forKey: "Tap")
        }
    }
    
}


// AppStorage

struct ContentView: View {
    //Our access to the UserDefaults system is through the @AppStorage property wrapper. This works like @State: when the value changes, it will reinvoked the body property so our UI reflects the new data.

    //We attach a string name, which is the UserDefaults key where we want to store the data. I’ve used “tapCount”, but it can be anything at all – it doesn’t need to match the property name.

    //The rest of the property is declared as normal, including providing a default value of 0. That will be used if there is existing value saved inside UserDefaults.
    @AppStorage("tapCount") private var tapCount = 0
        
    var body: some View {
        Button("Tap Count: \(tapCount)") {
            tapCount += 1
        }
    }
    
}

```
