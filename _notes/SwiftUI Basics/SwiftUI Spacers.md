---
title: SwiftUI Spacers
---

### Main Idea
Spacers can be used to push align views horizontally or vertically. Spacer determines it's spacing of free space according to the number of spacer(). 


```swift
var body: some View {
    Spacer() 
    
    VStack {
        Text("Hello, world!")
        Text("This is inside a stack")
    }
    Spacer()
    Spacer()
    
    Text("Hello")
    Spacer()
}

```


