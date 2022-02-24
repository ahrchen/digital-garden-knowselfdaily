---
title: SwiftUI Alerts
---

### Main Idea
If something important happens, a common way of notifying the user is using an alert – a pop up window that contains a title, message, and one or two buttons depending on what you need.

```swift
struct ContentView: View {
// We then attach our alert somewhere to our user interface, telling it to use that state to determine whether the alert is presented or not. SwiftUI will watch showingAlert, and as soon as it becomes true it will show the alert.

    @State private var showingAlert = false

    var body: some View {
        Button("Show Alert") {
            showingAlert = true
        }
        //  two-way data binding because SwiftUI will automatically set showingAlert back to false when the alert is dismissed.
        .alert("Important message", isPresented: $showingAlert) {
            Button("OK") { }
        }
    }
}

// Add more buttons 
.alert("Important message", isPresented: $showingAlert) {
    Button("Delete", role: .destructive) { }
    Button("Cancel", role: .cancel) { }
}

// Add message 
Button("Show Alert") {
    showingAlert = true
}
.alert("Important message", isPresented: $showingAlert) {
    Button("OK", role: .cancel) { }
} message: {
    Text("Please read this.")
}
```


