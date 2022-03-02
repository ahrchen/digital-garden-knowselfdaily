---
title: SwiftUI ImagePaint
---

### Main Idea

ImagePaint SwiftUI gives us a dedicated type that wraps images in a way that we have complete control over how borders should be rendered

```swift

Capsule()
    .strokeBorder(ImagePaint(image: Image("Example"), scale: 0.1), lineWidth: 20)
    .frame(width: 300, height: 300)


Text("Hello World")
    .frame(width: 300, height: 300)
    .border(ImagePaint(image: Image("Example"), sourceRect: CGRect(x: 0, y: 0.25, width: 1, height: 0.5), scale: 0.1), width: 30)


```
