---
title: SwiftUI Environment Wrapper
---

### Main Idea
 @Environment, and it allows us to create properties that store values provided to us externally. Is the user in light mode or dark mode? Have they asked for smaller or larger fonts? What timezone are they on? All these and more are values that come from the environment, and in this instance we’re going to ask the environment to dismiss our view.


### Usage

```swift
struct SecondView: View {
    @Environment(\.dismiss) var dismiss
    let name: String
    
    var body: some View {
        Button("Dismiss") {
            dismiss()
        }
    }
}

struct ContentView: View {
    @State private var showingSheet = false
    
    var body: some View {
        Button("Show Sheet") {
            showingSheet.toggle()
        }
        .sheet(isPresented: $showingSheet) {
            SecondView(name: "@two")
        }
    }
}
```
