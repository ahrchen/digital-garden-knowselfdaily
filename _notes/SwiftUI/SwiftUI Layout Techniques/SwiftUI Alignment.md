---
title: SwiftUI Alignment
---

### Main Idea

The simplest alignment option is to use the alignment parameter of a frame() modifier. Remember, a text view always uses the exact width and height required to show its text,
```swift 
Text("Live long and prosper")
    .frame(width: 300, height: 300)
```
Align Text to the text on the baseline of the last or first child in HStack
```swift
struct ContentView: View {
    var body: some View {
        HStack(alignment: .lastTextBaseline) {
            Text("Live")
                .font(.caption)
                Text("long")
                Text("and")
            Text("Prosper")
                .font(.largeTitle)
        }
    }
}
```

Now, when the VStack comes to aligning each of those text views, it asks them to provide their leading edge. By default this is obvious: it uses either the left or right edge of the view, depending on the system language. But what if we wanted to change that – what if we wanted to make one view have a custom alignment?

SwiftUI provides us with the alignmentGuide() modifier for just this purpose. This takes two parameters: the guide we want to change, and a closure that returns a new alignment. The closure is given a ViewDimensions object that contains the width and height of its view, along with the ability to read its various edges.

```swift
struct ContentView: View {
    var body: some View {
        VStack(alignment: .leading) {
            Text("Hello, world!")
                .alignmentGuide(.leading) { d in d[.trailing] }
            Text("This is a longer line of text")
        }
        .background(.red)
        .frame(width: 400, height: 400)
        .background(.blue)
    }
}

struct ContentView: View {
    var body: some View {
        VStack(alignment: .leading) {
            ForEach(0..<10) { position in
                
                Text("Number \(position)")
                    .alignmentGuide(.leading) { _ in CGFloat(position) * -10}
            }
        }
        .background(.red)
        .frame(width: 400, height: 400)
        .background(.blue)
        
    }
}

```
