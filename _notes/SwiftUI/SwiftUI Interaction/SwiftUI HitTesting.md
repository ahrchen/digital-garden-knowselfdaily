---
title: SwiftUI HitTesting
---

### Main Idea

SwiftUI has an advanced hit testing algorithm that uses both the frame of a view and often also its contents. We can customize that.

BASIC
```swift
ZStack {
    Rectangle()
        .fill(.blue)
        .frame(width: 300, height: 300)
        .onTapGesture {
            print("Rectangle tapped!")
        }

    Circle()
        .fill(.red)
        .frame(width: 300, height: 300)
        .onTapGesture {
            print("Circle tapped!")
        }
}
```
ONLY RECTANGLE
```swift
ZStack {
    Rectangle()
        .fill(.blue)
        .frame(width: 300, height: 300)
        .onTapGesture {
            print("Rectangle tapped!")
        }

    Circle()
        .fill(.red)
        .frame(width: 300, height: 300)
        .onTapGesture {
            print("Circle tapped!")
        }
        .allowHitTesting(false)
}
```

ONLY CIRCLE
```swift
ZStack {
    Rectangle()
        .fill(.blue)
        .frame(width: 300, height: 300)
        .onTapGesture {
            print("Rectangle tapped!")
        }

    Circle()
        .fill(.red)
        .frame(width: 300, height: 300)
        .contentShape(Rectangle())
        .onTapGesture {
            print("Circle tapped!")
        }
}
```

Entire VSTACK
```swift
VStack {
    Text("Hello")
    Spacer().frame(height: 100)
    Text("World")
}
.contentShape(Rectangle())
.onTapGesture {
    print("VStack tapped!")
}
```
