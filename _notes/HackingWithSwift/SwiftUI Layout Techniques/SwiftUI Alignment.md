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
