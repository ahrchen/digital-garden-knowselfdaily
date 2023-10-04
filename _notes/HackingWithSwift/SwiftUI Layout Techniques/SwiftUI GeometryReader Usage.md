---
title: SwiftUI GeometryReader Usage
---

### Main Idea

Previously we used DragGesture to store a width and height as an @State property, because it allowed us to adjust other properties based on the drag amount to create neat effects. However, with GeometryReader we can grab values from a view’s environment dynamically, feeding in its absolute or relative position into various modifiers. Even better, you can nest geometry readers if needed, so that one can read the geometry for a higher-up view and the other can read the geometry for something further down the tree.

To try some effects with GeometryReader, we could create a spinning helix effect by creating 50 text views in a vertical scroll view, each of which an infinite maximum width so they take up all the screen space, then apply a 3D rotation effect based on their own position.

```swift 
struct ContentView: View {
    let colors: [Color] = [.red, .green, .blue, .orange, .pink, .purple, .yellow]
    var body: some View {
        GeometryReader { fullView in
            ScrollView {
                ForEach(0..<50) { index in
                    GeometryReader { geo in
                        Text("Row #\(index)")
                            .font(.title)
                            .frame(maxWidth: .infinity)
                            .background(colors[index % 7])
                            .rotation3DEffect(.degrees(geo.frame(in: .global).minY - fullView.size.height / 2) / 5, axis: (x:0, y:1, z: 0))
                    }
                    .frame(height:40)
                }
            }
            
        }
    }
}
```
We can use a similar technique to create CoverFlow-style scrolling rectangles:
```swift 
struct ContentView: View {
    var body: some View {
        GeometryReader { fullView in
            ScrollView(.horizontal, showsIndicators: false) {
                HStack(spacing: 0) {
                    ForEach(1..<20) { num in
                        GeometryReader { geo in
                            Text("Number \(num) ")
                                .font(.largeTitle)
                                .padding()
                                .background(.red)
                                .rotation3DEffect((.degrees(-geo.frame(in: .global).minX + fullView.size.width / 2 - geo.size.width / 2) / 4) , axis: (x:0, y:1, z:0))
                                .frame(width: 200, height: 200)
                        }
                        .frame(width: 200, height: 200)
                    }
                }
            }
        }
    }
}
```
