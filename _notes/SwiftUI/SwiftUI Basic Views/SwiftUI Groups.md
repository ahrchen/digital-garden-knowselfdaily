---
title: SwiftUI Groups
---

### Main Idea
Group view help us group views together to get around the 10 views per parent limit, it also acts a a transparent layout container 
1. It does not affect our layout at all
2. it gives us the ability to add SwiftUI modifiers as needed, without @ViewBuilder 

That group contains no layout information, so we don’t know whether the three text fields will be stacked vertically, horizontally, or by depth. This is where the transparent layout behavior of Group becomes important: whatever parent places a UserView gets to decide how its text views get arranged.

see https://www.hackingwithswift.com/books/ios-swiftui/using-groups-as-transparent-layout-containers
```swift
struct UserView: View {
    var body: some View {
        Group {
            Text("Name: Paul")
            Text("Country: England")
            Text("Pets: Luna and Arya")
        }
        .font(.title)
    }
}

struct ContentView: View {
    @State private var layoutVertically = false

    var body: some View {
        Group {
            if layoutVertically {
                VStack {
                    UserView()
                }
            } else {
                HStack {
                    UserView()
                }
            }
        }
        .onTapGesture {
            layoutVertically.toggle()
        }
    }
}
```

or

```swift
struct ContentView: View {
    @Environment(\.horizontalSizeClass) var sizeClass
    
    var body: some View {
        if sizeClass == .compact {
            VStack(content: UserView.init)
        } else {
            HStack(content: UserView.init)
        }
    }
}
```
Regardless of whether we’re toggling our layout using size classes or tap gestures, the point is that UserView just doesn’t care – its Group simply groups the text views together without affecting their layout at all, so the layout arrangement UserView is given depends entirely on how it’s used.
