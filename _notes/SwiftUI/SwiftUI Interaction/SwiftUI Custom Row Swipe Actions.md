---
title: SwiftUI Custom Row Swipe Actions
---

### Main Idea

iOS apps have had “swipe to delete” functionality for as long as I can remember, but in more recent years they’ve grown in power so that list rows can have multiple buttons, often on either side of the row. We get this full functionality in SwiftUI using the swipeActions() modifier, which lets us register one or more buttons on one or both sides of a list row.

You can customize edge where they your buttons are placed by providing an edge parameter to your swipeActions() modifier, and you can customize the color of your buttons either by adding a tint() modifier to them with a color of your choosing, or by attaching a button role.

So, this will display one button on either side of our row:

Referenced from  https://www.hackingwithswift.com/books/ios-swiftui/adding-custom-row-swipe-actions-to-a-list
```swift
struct ContentView: View {
    
    var body: some View {
        List {
            Text("Taylor Swift")
                .swipeActions {
                    Button(role: .destructive) {
                        print("hi")
                    } label: {
                        Label("Delete", systemImage: "minus.circle")
                    }
                }
                .swipeActions(edge: .leading) {
                    Button {
                        print("hi")
                    } label: {
                        Label("Pin", systemImage: "pin")
                    }
                    .tint(.orange)
                }
        }
    }
}
```
