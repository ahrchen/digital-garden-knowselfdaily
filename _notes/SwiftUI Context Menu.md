---
title: SwiftUI Context Menu
---

### Main Idea

We use context menu to offer addition features to the user upon clicking an item.
Rules to keep in mind:
1. If you're going to use it, use it on all items. Kinda of annoying if it only kinda works
2. Keep the list of options short 2 - 3 options
3. Self Contained options. Should not be anywhere else  

```swift
struct ContentView: View {
    
    enum BackgroundColorSelection {
        case red, green, blue
    }
    @State private var backgroundColor = Color.red
    @State private var backgroundColorSelection = BackgroundColorSelection.red
    
    var body: some View {
        VStack {
            Text("Hello World!")
                .padding()
                .background(backgroundColor)
            
            Text("Change Color")
                .padding()
                .contextMenu {
                    Button {
                        backgroundColor = .red
                        backgroundColorSelection = .red
                    } label: {
                        backgroundColorSelection == .red ?
                        Label("Red", systemImage: "checkmark.circle.fill")
                            .foregroundColor(.red) :
                        Label("Red", systemImage:"")
                            .foregroundColor(.red)
                    }
                    
                    Button {
                        backgroundColor = .green
                        backgroundColorSelection = .green
                    } label: {
                        backgroundColorSelection == .green ?
                        Label("Green", systemImage: "checkmark.circle.fill")
                            .foregroundColor(.green) :
                        Label ("Green", systemImage: "")
                            .foregroundColor(.green)
                    }
                    
                    Button {
                        backgroundColor = .blue
                        backgroundColorSelection = .blue
                    } label: {
                        backgroundColorSelection == .blue ?
                        Label("Blue", systemImage: "checkmark.circle.fill")
                            .foregroundColor(.blue) :
                        Label("Blue", systemImage: "")
                            .foregroundColor(.blue)
                    }
                }
        }
        
    }
    
}



```
