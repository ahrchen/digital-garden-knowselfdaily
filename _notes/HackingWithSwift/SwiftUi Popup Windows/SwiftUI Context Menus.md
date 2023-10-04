---
title: SwiftUI Context Menu
---

### Main Idea

When the user taps a button or a navigation link, it’s pretty clear that SwiftUI should trigger the default action for those views. But what if they press and hold on something? On older iPhones users could trigger a 3D Touch by pressing hard on something, but the principle is the same: the user wants more options for whatever they are interacting with.

SwiftUI lets us attach context menus to objects to provide this extra functionality, all done using the contextMenu() modifier. You can pass this a selection of buttons and they’ll be shown in order, so we could build a simple context menu to control a view’s background color like this:

I have a few tips for you when working with context menus, to help ensure you give your users the best experience:

1. If you’re going to use them, use them in lots of places – it can be frustrating to press and hold on something only to find nothing happens.
2. Keep your list of options as short as you can – aim for three or less.
3. Don’t repeat options the user can already see elsewhere in your UI.

Remember, context menus are by their nature hidden, so please think twice before hiding important actions in a context menu.

<img src="/assets/ContextMenuImage.png"/>

Referenced from https://www.hackingwithswift.com/books/ios-swiftui/creating-context-menus
```swift
struct ContentView: View {
    @State private var backgroundColor = Color.red
    
    var body: some View {
        VStack {
            Text("Hello, World!")
                .padding()
                .background(backgroundColor)
            
            Text("Change Color")
                .padding()
                .contextMenu {
                    Button {
                        backgroundColor = .red
                    } label: {
                        Label("Red", systemImage: backgroundColor == .red ? "checkmark.circle.fill" : "checkmark.circle")
                    }
                    
                    Button {
                        backgroundColor = .green
                    } label: {
                        Label("Green", systemImage: backgroundColor == .green ? "checkmark.circle.fill" : "checkmark.circle")
                    }
                    
                    Button {
                        backgroundColor = .blue
                    } label: {
                        Label("Blue", systemImage: backgroundColor == .blue ? "checkmark.circle.fill" : "checkmark.circle")
                        }
                }
        }
    }
}
```
