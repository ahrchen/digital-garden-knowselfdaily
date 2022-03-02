---
title: SwiftUI Paths
---

### Main Idea

SwiftUI gives us a dedicated Path type for drawing custom shapes. It’s very low level, by which I mean you will usually want to wrap it in something else in order for it to be more useful, but as it’s the building block that underlies other work we’ll do we’re going to start there.Just like colors, gradients, and shapes, paths are views in their own right. This means we can use them just like text views and images, although as you’ll see it’s a bit clumsy.

```swift

// drawing a triangle
struct ContentView: View {
    var body: some View {
        Path { path in
            path.move(to: CGPoint(x: 200, y: 100))
            path.addLine(to: CGPoint(x: 100, y: 300))
            path.addLine(to: CGPoint(x: 300, y: 300))
            path.addLine(to: CGPoint(x: 200, y: 100))
//            path.closeSubpath()
        }
        .stroke(.blue, style: StrokeStyle(lineWidth: 10,lineCap: .round, lineJoin: .round))
    }
}
```
