---
title: SwiftUI FocusState Wrapper
---

### Main Idea

SwiftUI gives us a specific property wrapper for tracking which view currently receives user input, called @FocusState. This can be bound to a Boolean to control a single field, or to an enum to control movement between several.


### Usage

```swift
// If you just want to control whether a single piece of input has keyboard focus you can use this with a Boolean like this:

struct ContentView: View {
    @FocusState private var isUsernameFocused: Bool
    @State private var username = "Anonymous"

    var body: some View {
        VStack {
            TextField("Enter your username", text: $username)
                .focused($isUsernameFocused)

            Button("Toggle Focus") {
                isUsernameFocused.toggle()
            }
        }
    }
}

// If you want to move keyboard focus between more than one view you should use an optional enum. This can be set to one of the cases from your enum to activate a particular piece of input, or you can set it to nil to make nothing focused – effectively dismissing the keyboard on iOS.

// So, we could create two text fields to store a username and password, then move between them using @FocusState and onSubmit():

struct ContentView: View {
    enum FocusedField {
        case username, password
    }

    @FocusState private var focusedField: FocusedField?
    @State private var username = "Anonymous"
    @State private var password = "sekrit"

    var body: some View {
        VStack {
            TextField("Enter your username", text: $username)
                .focused($focusedField, equals: .username)

            SecureField("Enter your password", text: $password)
                .focused($focusedField, equals: .password)
        }
        .onSubmit {
            if focusedField == .username {
                focusedField = .password
            } else {
                focusedField = nil
            }
        }
    }
}
```
