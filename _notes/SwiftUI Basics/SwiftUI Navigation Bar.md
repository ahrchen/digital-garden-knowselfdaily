---
title: SwiftUI Navigation Bar
---

### Main Idea
Navigation bars can have titles and buttons, and in SwiftUI they also give us the ability to display new views when the user performs an action. it makes our form look better when it scrolls.


```swift
NavigationView {
    Form {
        Section {
            Text("Hello, world!")
        }
    }
    // Set navigation Bar title
    .navigationTitle("SwiftUI")
    // Smaller navigation bar title 
    .navigationBarTitleDisplayMode(.inline)
}

```


