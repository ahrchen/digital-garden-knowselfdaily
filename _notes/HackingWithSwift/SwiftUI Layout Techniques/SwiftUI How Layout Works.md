---
title: SwiftUI How Layout Works
---

### Main Idea

All SwiftUI layout happens in three simple steps, and understanding these steps is the key to getting great layouts every time. The steps are:

1. A parent view proposes a size for its child.
2. Based on that information, the child then chooses its own size and the parent must respect that choice.
3. The parent then positions the child in its coordinate space.

for more detail see https://www.hackingwithswift.com/books/ios-swiftui/how-layout-works-in-swiftui

```swift
Text("Hello, World!")
    .padding(20)
    .background(.red)
```

SwiftUI: You can have the whole screen, how much of it do you need, ContentView?
ContentView: You can have the whole screen, how much of it do you need, background?
Background: You can have the whole screen, how much of it do you need, padding?
Padding: You can have the whole screen minus 20 points on each side, how much of it do you need, text?
Text: I need X by Y.
Padding: I need X by Y plus 20 points on each side.
Background: I need X by Y plus 20 points on each side.
ContentView: I need X by Y plus 20 points on each side.
SwiftUI: OK; I’ll center you.

