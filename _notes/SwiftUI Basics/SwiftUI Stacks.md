---
title: SwiftUI Stacks
---

### Main Idea
Stacks help us group view horizontally, vertical, and depth with HStack, VStack, and ZStack respectively


```swift
var body: some View {
    VStack {
        Text("Hello, world!")
        Text("This is inside a stack")
    }
}

// ZStack draws its contents from top to bottom, back to front. This means if you have an image then some text ZStack will draw them in that order, placing the text on top of the image.
ZStack {
    Text("Hello, world!")
    Text("This is inside a stack")
}

```


