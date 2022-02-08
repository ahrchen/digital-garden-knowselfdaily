---
title: SwiftUI Buttons
---

### Main Idea
SwiftUI buttons,  it just contains some text you pass in the title of the button, along with a closure that should be run when the button is tapped:

```swift
struct ContentView: View {
    var body: some View {
        Button("Delete selection", action: executeDelete)
    }

    func executeDelete() {
        print("Now deleting…")
    }
}
// Modify Role
Button("Delete selection", role: .destructive, action: executeDelete)
// Modify styles 
VStack {
    Button("Button 1") { }
        .buttonStyle(.bordered)
    Button("Button 2", role: .destructive) { }
        .buttonStyle(.bordered)
    Button("Button 3") { }
        .buttonStyle(.borderedProminent)
        // color it a bit
        .tint(.mint)
    Button("Button 4", role: .destructive) { }
        .buttonStyle(.borderedProminent)
}


// Custom Buttons 
Button {
    print("Button was tapped")
} label: {
    Text("Tap me!")
        .padding()
        .foregroundColor(.white)
        .background(.red)
}

// Images
Button {
    print("Edit button was tapped")
} label: { 
    Image(systemName: "pencil")
    // Don't say anything about it use decorative
    Image(decorative: "pencil")
}

Button {
    print("Edit button was tapped")
} label: {
    Label("Edit", systemImage: "pencil")
}

// Use modifier renderingMode(.original) to remove solid blue Swiftui used to show that they are tappable
renderingMode(.original)
```


