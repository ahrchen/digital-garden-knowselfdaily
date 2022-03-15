---
title: SwiftUI TextEditor
---

### Main Idea

We’ve used SwiftUI’s TextField view several times already, and it’s great for times when the user wants to enter short pieces of text. However, for longer pieces of text you should switch over to using a TextEditor view instead: it also expects to be given a two-way binding to a text string, but it has the additional benefit of allowing multiple lines of text – it’s much better for accepting longer strings from the user.


```swift
struct ContentView: View {
    @AppStorage("notes") private var notes = ""
    
    var body: some View {
        NavigationView {
            TextEditor(text: $notes)
                .navigationTitle("Notes")
                .padding()
        }
    }
}
```


