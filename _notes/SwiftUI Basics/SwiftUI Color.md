---
title: SwiftUI Color
---

### Main Idea
Color.red is a view in itself, can be used like Text. The frame modifier specify the size of the color.aaa

```swift
var body: some View {
    ZStack {
        Color.red
        .frame(width: 200, height: 200)
        
        Text("Your content")
    }
    
    // Light And Dark Mode
    ZStack {
        Color.primary
    }
    
    // Transparent layer 
    ZStack {
        Color.secondary
    }
    
    // Custom
    ZStack {
        Color(red: 1, green: 0.8, blue: 0)
    }
    
    //ignoresSafeArea() to fill in the entire screen 
    ZStack {
        Color(red: 1, green: 0.8, blue: 0)
    }
    .ignoresSafeArea()
    
    
    ZStack {
    VStack(spacing: 0) {
        Color.red
        Color.blue
    }   

    Text("Your content")
        .foregroundColor(.secondary)
        //Or let the background shine through
        .foregroundStyle(.secondary)
        .padding(50)
        .background(.ultraThinMaterial)
}
.ignoresSafeArea()

// Semantic colors are colors that are named according to their use rather than according to their hue.
// Primary, Secondary, Tertiary, and Quaternary text style variants of all text styles
Color.primary
Color.secondary


```


