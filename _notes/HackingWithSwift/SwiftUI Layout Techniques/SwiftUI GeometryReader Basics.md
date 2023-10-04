---
title: SwiftUI GeometryReader Basics
---

### Main Idea

SwiftUI’s GeometryReader allows us to use its size and coordinates to determine a child view’s layout, and it’s the key to creating some of the most remarkable effects in SwiftUI.

To understand what’s happening here you need to remember the three step layout process of SwiftUI:

1. A parent view proposes a size for its child.
2. Based on that information, the child then chooses its own size and the parent must respect that choice.
3. The parent then positions the child in its coordinate space.

```swift 
GeometryReader { geo in
    Text("Hello, World!")
        .frame(width: geo.size.width * 0.9)
        .background(.red)
}
```
GeometryReader has an interesting side effect that might catch you out at first: the view that gets returned has a flexible preferred size, which means it will expand to take up more space as needed. You can see this in action if you place the GeometryReader into a VStack then put some more text below it, like this:
```swift
struct OuterView: View {
    var body: some View {
        VStack {
           Text("Top")
            InnerView()
                .background(.green)
            Text("Bottom")
        }
        
            
    }
}

struct InnerView: View {
    var body: some View {
        HStack {
            Text("Left")
            GeometryReader { geo in
                Text("Center")
                    .background(.blue)
                    .onTapGesture {
                        print("Global center: \(geo.frame(in: .global).midX) x \(geo.frame(in: .global).midY))")
                        print("Local center: \(geo.frame(in: .local).midX) x \(geo.frame(in: .local).midY))")
                        print("Custom center: \(geo.frame(in: .named("Custom")).midX) x \(geo.frame(in: .named("Custom")).midY))")
                    }
            }
            .background(.orange)
            Text("Right")
        }
    }
}

struct ContentView: View {
    var body: some View {
        OuterView()
            .background(.red)
            .coordinateSpace(name: "Custom")
    }
}
```

Which coordinate space you want to use depends on what question you want to answer:

Want to know where this view is on the screen? Use the global space.
Want to know where this view is relative to its parent? Use the local space.
What to know where this view is relative to some other view? Use a custom space.
