---
title: SwiftUI Multiple Views Side by Side
---

### Main Idea

SwiftUI autogenerates a second or third view for us, when using a device with a certain with.

for more detail see https://www.hackingwithswift.com/books/ios-swiftui/working-with-two-side-by-side-views-in-swiftui

```swift
struct ContentView: View {
    var body: some View {
        NavigationView {
            NavigationLink {
                Text("New secondary!")
            } label: {
                Text("Hello world!")
            }
            .navigationTitle("Primary")
            Text("Secondary")
            
            Text("Tertiary")
        }
    }
}

```


