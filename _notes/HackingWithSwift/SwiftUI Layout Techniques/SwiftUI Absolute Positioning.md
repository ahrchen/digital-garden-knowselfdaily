---
title: SwiftUI Absolute Positioning
---

### Main Idea

To understand what’s happening here you need to remember the three step layout process of SwiftUI:

A parent view proposes a size for its child.
Based on that information, the child then chooses its own size and the parent must respect that choice.
The parent then positions the child in its coordinate space.

```swift 

Text("Hello, world!")
    .background(.red)
    .position(x: 100, y: 100)
    
// VS
Text("Hello world")
    .position(x: 100, y: 100)
    .background(.red)
```

Let try offset, offset shift the location of the view unlike position which sets the location.
When we use the offset() modifier, we’re changing the location where a view should be rendered without actually changing its underlying geometry. This means when we apply background() afterwards it uses the original position of the text, not its offset. If you move the modifier order so that background() comes before offset() then things work more like you might have expected, showing once again that modifier order matters.
```swift
Text("Hello world")
    .background(.red)
    .offset(x: 100, y: 100)

// VS

Text("Hello world")
    .offset(x: 100, y: 100)
    .background(.red)
```
