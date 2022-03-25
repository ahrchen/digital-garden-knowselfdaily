---
title: SwiftUI Drawing Special Effects
---

### Main Idea

SwiftUI gives us extraordinary control over how views are rendered, including the ability to apply real-time blurs, blend modes, saturation adjustment, and more.

Blend modes allow us to control the way one view is rendered on top of another. The default mode is .normal, which just draws the pixels from the new view onto whatever is behind, but there are lots of options for controlling color and opacity.

There are a host of other real-time effects we can apply, and we already looked at blur() back in project 3. So, let’s look at just one more before we move on: saturation(), which adjusts how much color is used inside a view. Give this a value between 0 (no color, just grayscale) and 1 (full color).

```swift
// BlendMode
struct ContentView: View {
    @State private var amount = 0.0
    
    var body: some View {
        VStack {
            ZStack {
                Circle()
                    .fill(Color(red: 1, green: 0, blue: 0))
                    .frame(width: 200 * amount)
                    .offset(x: -50, y: -80)
                    .blendMode(.screen)
                Circle()
                    .fill(Color(red: 0, green: 1, blue: 0))
                    .frame(width: 200 * amount)
                    .offset(x: 50, y: -80)
                    .blendMode(.screen)
                Circle()
                    .fill(Color(red: 0, green: 0, blue: 1))
                    .frame(width: 200 * amount)
                    .blendMode(.screen)
            }
            .frame(width: 300, height: 300)
                
            Slider(value: $amount)
                .padding()
        }
        .frame(maxWidth: .infinity, maxHeight: .infinity)
        .background(.black)
        .ignoresSafeArea()
    }
}
// Blur and Saturation 
// With that code, having the slider at 0 means the image is blurred and colorless, but as you move the slider to the right it gains color and becomes sharp – all rendered at lightning-fast speed.

struct ContentView: View {
    @State private var amount = 0.0
    
    var body: some View {
        VStack {
            Image("Example")
                .resizable()
                .scaledToFit()
                .frame(width: 200, height: 200)
                .saturation(amount)
                .blur(radius: (1 - amount) * 20)
            
            Slider(value: $amount)
                .padding()
        }
    }
}

```
