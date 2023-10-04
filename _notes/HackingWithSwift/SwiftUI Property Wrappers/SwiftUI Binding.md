---
title: SwiftUI Binding
---

### Main Idea

In summary, I want this struct variable to be passed by reference. 

#### In long:
You’ve already seen how SwiftUI’s @State property wrapper lets us work with local value types, and how @StateObject lets us work with shareable reference types. Well, there’s a third option, called @Binding, which lets us connect an @State property of one view to some underlying model data.

That’s where @Binding comes in: it lets us store a mutable value in a view that actually points to some other value from elsewhere. In the case of Toggle, the switch changes its own local binding to a Boolean, but behind the scenes that’s actually manipulating the @State property in our view.

This makes @Binding extremely important for whenever you want to create a custom user interface component. At their core, UI components are just SwiftUI views like everything else, but @Binding is what sets them apart: while they might have their local @State properties, they also expose @Binding properties that let them interface directly with other views.

it allows us to create a two-way connection between PushButton and whatever is using it, so that when one value changes the other does too.

This is the power of @Binding: as far as the button is concerned it’s just toggling a Boolean – it has no idea that something else is monitoring that Boolean and acting upon changes.

### Usage

```swift

struct PushButton: View {
    let title: String
    @Binding var isOn: Bool
    
    var onColors = [Color.red, Color.yellow]
    var offColors = [Color(white: 0.6), Color(white:0.4)]
    
    var body: some View {
        Button(title) {
            isOn.toggle()
        }
        .padding()
        .background(LinearGradient(gradient: Gradient(colors: isOn ? onColors : offColors), startPoint: .top, endPoint: .bottom))
        .foregroundColor(.white)
        .clipShape(Capsule())
        .shadow(radius: isOn ? 0 : 5)
    }
}

struct ContentView: View {
    @State private var rememberMe = false
    
    var body: some View {
        VStack {
            PushButton(title: "Remember Me", isOn: $rememberMe)
            Text(rememberMe ? "On" : "Off")
        }
    }
}
```
