---
title: SwiftUI State Wrapper
---

### Main Idea

SwiftUI uses the @State property wrapper to allow us to modify values inside a struct, which would normally not be allowed because structs are value types.

When we put @State before a property, we effectively move its storage out from our struct and into shared storage managed by SwiftUI. This means SwiftUI can destroy and recreate our struct whenever needed (and this can happen a lot!), without losing the state it was storing.

Use onChange() to watch for changes to the State Wrapper and respond to state changes

### Usage

```swift
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
```
