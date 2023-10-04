---
title: SwiftUI Stepper
---

### Main Idea
Stepper: a simple - and + button that can be tapped to select a precise number. We can set a range and step. 


```swift
struct ContentView: View {
    
    @State private var sleepAmount = 8.0
    
    var body: some View {
        Stepper("\(sleepAmount.formatted()) hours", value: $sleepAmount, in: 4...12, step: 0.25)
    }
}
```


