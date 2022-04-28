---
title: SwiftUI Slider
---

### Main Idea
Slider: a simple way to adjest continous values.
- Value: What Double to bind it to.
- In: The range of the slider.
- Step: How much to change the value when you move the slider. This parameter is optional.

<img src="/assets/slider_example.gif"/>
```swift
struct ContentView: View {
    @State private var minutes: Double = 0
    @State private var hours: Double = 1
    
    var body: some View {
        VStack {
            Slider(value: $hours, in: 0...23, step: 1.0)
            Slider(value: $minutes, in: 0...59, step: 1.0)
            Text("\(hours, specifier: "%.0f") \(hours == 1.0 ? "Hour" : "Hours") and \(minutes, specifier: "%.0f") \(minutes == 1.0 ? "Minute" :"Minutes")")
        }
        
    }
}
```


