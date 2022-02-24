---
title: SwiftUI Grid
---

### Main Idea
SwiftUI’s List view is a great way to show scrolling rows of data, but sometimes you also want columns of data – a grid of information, that is able to adapt to show more data on larger screens.

In SwiftUI this is accomplished with two views: LazyHGrid for showing horizontal data, and LazyVGrid for showing vertical data. Just like with lazy stacks, the “lazy” part of the name is there because SwiftUI will automatically delay loading the views it contains until the moment they are needed, meaning that we can display more data without chewing through a lot of system resources.

```swift
struct ContentView: View {
    let layout = [
        GridItem(.adaptive(minimum: 80, maximum: 120)),
    ]
    var body: some View {
        ScrollView(.horizontal) {
            LazyHGrid(rows: layout) {
                ForEach(0..<1000) {
                    Text("Item \($0)")
                }
            }
        }
    }
}
```


