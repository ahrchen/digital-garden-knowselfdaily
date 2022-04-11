---
title: SwiftUI Gestures Advanced
---

### Main Idea
For more advanced gestures you should use the gesture() modifier with one of the gesture structs: DragGesture, LongPressGesture, MagnificationGesture, RotationGesture, and TapGesture. These all have special modifiers, usually onEnded() and often onChanged() too, and you can use them to take action when the gestures are in-flight (for onChanged()) or completed (for onEnded()).

```swift
struct ContentView: View {
    @State private var currentAmount = 0.0
    @State private var finalAmount = 1.0
    
    var body: some View {
        Text("Hello, world!")
            .scaleEffect(finalAmount + currentAmount)
            .gesture(
                MagnificationGesture()
                    .onChanged { amount in
                        currentAmount = amount - 1
                    }
                    .onEnded { amount in
                        finalAmount += currentAmount
                        currentAmount = 0 
                    }
            )
    }
}

struct ContentView: View {
    @State private var currentAmount = Angle.zero
    @State private var finalAmount =  Angle.zero
    
    var body: some View {
        Text("Hello, world!")
            .rotationEffect(currentAmount + finalAmount)
            .gesture(
                RotationGesture()
                    .onChanged { angle in
                        currentAmount = angle
                    }
                    .onEnded { angle in
                        finalAmount += currentAmount
                        currentAmount = .zero
                    }
            )
    }
}



```

