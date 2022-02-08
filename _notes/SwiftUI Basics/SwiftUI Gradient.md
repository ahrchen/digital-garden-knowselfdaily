---
title: SwiftUI Gradient
---

### Main Idea
SwiftUI gives us three kinds of gradients to work with, and like colors they are also views that can be drawn in our UI.

Gradients are made up of several components:

An array of colors to show
Size and direction information
The type of gradient to use


```swift
var body: some View {
// 1. Linear
    LinearGradient(gradient: Gradient(stops: [
        Gradient.Stop(color: .white, location: 0.45),
        Gradient.Stop(color: .black, location: 0.55),
    ]), startPoint: .top, endPoint: .bottom)
    
    // Simplify
    LinearGradient(gradient: Gradient(stops: [
        .init(color: .white, location: 0.45),
        .init(color: .black, location: 0.55),
    ]), startPoint: .top, endPoint: .bottom)
    
// 2. Radial
RadialGradient(gradient: Gradient(colors: [.blue, .black]), center: .center, startRadius: 20, endRadius: 200)

// 3. Angular
AngularGradient(gradient: Gradient(colors: [.red, .yellow, .green, .blue, .purple, .red]), center: .center)
}


```


