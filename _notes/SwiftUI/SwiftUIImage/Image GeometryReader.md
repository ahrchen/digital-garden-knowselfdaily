---
title: Image GeometryReader
---

### Main Idea

GeometryReader is a view just like the others we’ve used, except when we create it we’ll be handed a GeometryProxy object to use. This lets us query the environment: how big is the container? What position is our view? Are there any safe area insets? And so on.

In principle that seems simple enough, but in practice you need to use GeometryReader carefully because it automatically expands to take up available space in your layout, then positions its own content aligned to the top-left corner.


```swift
        GeometryReader { geo in
            Image("Raymond")
                .resizable()
                .scaledToFill()
                .frame(width: geo.size.width * 0.8)
                .frame(width:geo.size.width, height: geo.size.height)
        }
```
