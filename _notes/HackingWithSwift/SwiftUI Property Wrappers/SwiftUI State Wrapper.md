---
title: SwiftUI State Wrapper
---

### Main Idea

SwiftUI uses the @State property wrapper to allow us to modify values inside a struct, which would normally not be allowed because structs are value types.

When we put @State before a property, we effectively move its storage out from our struct and into shared storage managed by SwiftUI. This means SwiftUI can destroy and recreate our struct whenever needed (and this can happen a lot!), without losing the state it was storing.

A new Struct object is created each time the values in the struct changes.



### Usage

```swift

// Use onChange() to watch for changes to the State Wrapper and respond to state changes

struct ContentView: View {
    @State private var blurAmount = 0.0 
    
    var body: some View {
        Text("Hello, world!")
            .blur(radius: blurAmount)
        
        Slider(value: $blurAmount, in: 0...20)
        
        Button("Random Blur") {
            blurAmount = Double.random(in: 0...20)
        }
        .onChange(of: blurAmount) { newValue in
            print("New value is \(newValue)")
        }
    }
        
}

// Behind the scenes @State is actually just a binding 

struct ContentView: View {
    @State private var selection = 0

    var body: some View {
        let binding = Binding(
            get: { selection },
            set: { selection = $0 }
        )

        return VStack {
            Picker("Select a number", selection: binding) {
                ForEach(0..<3) {
                    Text("Item \($0)")
                }
            }
            .pickerStyle(.segmented)
        }
    }
}

// Usecase auto update three @state

@State var agreedToTerms = false
@State var agreedToPrivacyPolicy = false
@State var agreedToEmails = false

let agreedToAll = Binding(
    get: {
        agreedToTerms && agreedToPrivacyPolicy && agreedToEmails
    },
    set: {
        agreedToTerms = $0
        agreedToPrivacyPolicy = $0
        agreedToEmails = $0
    }
)

struct ContentView: View {
    @State private var agreedToTerms = false
    @State private var agreedToPrivacyPolicy = false
    @State private var agreedToEmails = false

    var body: some View {
        let agreedToAll = Binding<Bool>(
            get: {
                agreedToTerms && agreedToPrivacyPolicy && agreedToEmails
            },
            set: {
                agreedToTerms = $0
                agreedToPrivacyPolicy = $0
                agreedToEmails = $0
            }
        )

        return VStack {
            Toggle("Agree to terms", isOn: $agreedToTerms)
            Toggle("Agree to privacy policy", isOn: $agreedToPrivacyPolicy)
            Toggle("Agree to receive shipping emails", isOn: $agreedToEmails)
            Toggle("Agree to all", isOn: agreedToAll)
        }
    }
}
```
