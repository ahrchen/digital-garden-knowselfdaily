---
title: SwiftUI Gestures Basic
---

### Main Idea
SwiftUI gives us lots of gestures for working with views, and does a great job of taking away most of the hard work so we can focus on the parts that matter. Easily the most common is our friend onTapGesture(), but there are several others, and there are also interesting ways of combining gestures together that are worth trying out.

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .onTapGesture(count: 2) {
                print("Double Tapped!")
            }
    }
}

struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .onLongPressGesture(minimumDuration: 2) {
                print("Long Tapped!")
            }
    }
}

struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .onLongPressGesture(minimumDuration: 2) {
                print("Long Tapped!")
            } onPressingChanged: { inProgress in
                print("In Progress: \(inProgress)!")
            }
    }
}


```

