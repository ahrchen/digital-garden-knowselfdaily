---
title: SwiftUI Confirmation Dialog
---

### Main Idea
If something important happens, a common way of notifying the user is using an confirmation dialog – a pop up window that contains a title, message, and a selection of buttons depending on what you need.

Reference: https://www.hackingwithswift.com/books/ios-swiftui/showing-multiple-options-with-confirmationdialog

```swift
struct ContentView: View {
    @State private var showingConfirmation = false
    @State private var backgroundColor = Color.white
    
    var body: some View {
        VStack {
            Text("Hello, World")
                .frame(width: 300, height: 300, alignment: .center)
                .background(backgroundColor)
                .onTapGesture {
                    showingConfirmation = true
                }
                .confirmationDialog("Change background", isPresented: $showingConfirmation) {
                    Button("Red") { backgroundColor = .red}
                    Button("Green") { backgroundColor = .green}
                    Button("Blue") {backgroundColor = .blue}
                    Button("Cancel", role: .cancel) {}
                    
                } message: {
                    Text("Select a new color")
                }
        }
    }
}
```


