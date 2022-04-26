---
title: SwiftUI ViewBuilder
---

### Main Idea
 
The @ViewBuilder property wrapper allows us to return different view types in a single view

The body property of any SwiftUI automatically gets the ability to return different views thanks to a special attributed called @ViewBuilder. This is implemented using Swift’s result builder system, and it understands how to present two different views depending on our app’s state.

However, this same functionality isn’t automatically everywhere, which means any custom properties you make must return the same view type.

### Usage
The following does not compile because tossResult cannot return Image or Text Views. So we wrap it in a Group
```swift
struct ContentView: View {
    var tossResult: some View {
        Group {
            if Bool.random() {
                Image("laser-show")
                    .resizable()
                    .scaledToFit()
            } else {
                Text("Better luck next time")
                    .font(.title)
            }
        }
        .frame(width: 400, height: 300)
    }

    var body: some View {
        VStack {
            Text("Coin Flip")
                .font(.largeTitle)

            tossResult
        }
    }
}
```
The following does not compile because tossResult cannot return Image or Text Views. So we wrap it in a TypeErasure AnyView() which is expensive.
```swift
struct ContentView: View {
    var tossResult: some View {
        if Bool.random() {
            return AnyView(Image("laser-show").resizable().scaledToFit())
        } else {
            return AnyView(Text("Better luck next time").font(.title))
        }
    }

    var body: some View {
        VStack {
            Text("Coin Flip")
                .font(.largeTitle)

            tossResult
                .frame(width: 400, height: 300)                
        }
    }
}
```
We can use @ViewBuilder for higher efficiency. 
```swift
struct ContentView: View {
    @ViewBuilder var tossResult: some View {
        if Bool.random() {
            Image("laser-show")
                .resizable()
                .scaledToFit()
        } else {
            Text("Better luck next time")
                .font(.title)
        }
    }

    var body: some View {
        VStack {
            Text("Coin Flip")
                .font(.largeTitle)

            tossResult
                .frame(width: 400, height: 300)                
        }
    }
}
Or just make a seperate view which is preferrable
```swift
struct TossResult: View {
    var body: some View {
        if Bool.random() {
            Image("laser-show")
                .resizable()
                .scaledToFit()
        } else {
            Text("Better luck next time")
                .font(.title)
        }
    }
}

struct ContentView: View {
    var body: some View {
        VStack {
            Text("Coin Flip")
                .font(.largeTitle)

            TossResult()
                .frame(width: 400, height: 300)
        }
    }
}
```
