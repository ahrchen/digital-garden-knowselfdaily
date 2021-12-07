---
title: Image Interpolation
---

### Main Idea

We use interpolation to determine the blending of small images in SwiftUI 

```swift
struct ContentView: View {
    
    var body: some View {
        Image("example")
            .interpolation(.none)
            .resizable()
            .scaledToFit()
            .frame(maxHeight: .infinity)
            .background(.black)
            .ignoresSafeArea()
        
    }
    
}


```
