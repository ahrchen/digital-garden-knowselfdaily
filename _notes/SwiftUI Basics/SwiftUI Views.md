---
title: SwiftUI Views And Modifiers
---

### Main Idea
Views are a generic form of the UI. Unlike UIKit where views are classes due to inheritance, views here are structs. 

Assume Modifiers creates a new view with that change applied so ORDER matters.

Opaque return types is used everytime we write some View. One object that conforms to the View protocol, but we don't want to say what. We are returning complex view with ModifiedContent and TupleView with multiple views inside.




How?

Why?
1. Views are struct because of Performance.
- Structs do not come with the baggage of inheritance

2. Views forces us to think about isolating state in a clean way. Functional design approach based on isolating states. Simpler to think about.


```swift
// Assume there is nothing behind our view. The view is our basecase.
Text("Hello, world!")
    .padding()
    .background(.red)
    
// --->
Text("Hello, world!")
    .frame(maxWidth: .infinity, maxHeight: .infinity)
    .background(.red)
    
// Example of ORDER modifier matters
Button("Hello, world!") {
    print(type(of: self.body))
}    
.background(.red)
.frame(width: 200, height: 200)
// ModifiedContent<ModifiedContent<Button<Text>, _BackgroundStyleModifier<Color>>, _FrameLayout>

Button("Hello, world!") {
    print(type(of: self.body))
}
.frame(width: 200, height: 200)
.background(.red)
ModifiedContent<ModifiedContent<Button<Text>, _FrameLayout>, _BackgroundStyleModifier<Color>>

Text("Hello, world!")
    .padding()
    .background(.red)
    .padding()
    .background(.blue)
    .padding()
    .background(.green)
    .padding()
    .background(.yellow)

ModifiedContent<ModifiedContent<ModifiedContent<ModifiedContent<ModifiedContent<ModifiedContent<ModifiedContent<ModifiedContent<Button<Text>, _PaddingLayout>, _BackgroundStyleModifier<Color>>, _PaddingLayout>, _BackgroundStyleModifier<Color>>, _PaddingLayout>, _BackgroundStyleModifier<Color>>, _PaddingLayout>, _BackgroundStyleModifier<Color>>


// Conditional Modifiers - use a tenary What do you want to check True False

struct ContentView: View {
    @State private var useRedText = false

    var body: some View {
        Button("Hello World") {
            // flip the Boolean between true and false
            useRedText.toggle()            
        }
        .foregroundColor(useRedText ? .red : .blue)
    }
}

// Environment modifiers - allows us to apply the same modifier to many views at the same time and override the effect while regular modifiers cannot, blur.

VStack {
    Text("Gryffindor")
        .font(.largeTitle)
    Text("Hufflepuff")
    Text("Ravenclaw")
    Text("Slytherin")
}
.font(.title)

// vs 
VStack {
    Text("Gryffindor")
        .blur(radius: 0)
    Text("Hufflepuff")
    Text("Ravenclaw")
    Text("Slytherin")
}
.blur(radius: 5)

// Views as properties, use computed properties so you can refer to other stored property, out of the three methods, @ViewBuilder because it mimics the way body works, 

var spells: some View {
    VStack {
        Text("Lumos")
        Text("Obliviate")
    }
}

var spells: some View {
    Group {
        Text("Lumos")
        Text("Obliviate")
    }
}

@ViewBuilder var spells: some View {
    Text("Lumos")
    Text("Obliviate")
}

// View Composition, store modifiers into views

struct CapsuleText: View {
    var text: String

    var body: some View {
        Text(text)
            .font(.largeTitle)
            .padding()
            .foregroundColor(.white)
            .background(.blue)
            .clipShape(Capsule())
    }
}

struct ContentView: View {
    var body: some View {
        VStack(spacing: 10) {
            CapsuleText(text: "First")
                .foregroundColor(.white)
            CapsuleText(text: "Second")
                .foregroundColor(.yellow)
        }
    }
}

// Custom modifiers

struct Title: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .foregroundColor(.white)
            .padding()
            .background(.blue)
            .clipShape(RoundedRectangle(cornerRadius: 10))
    }
}

struct ContentView: View {
    var body: some View {
        Text("Hello World")
            .modifier(Title())
    }
}


extension View {
    func titleStyle() -> some View {
        modifier(Title())
    }
}

// Afterwards 
Text("Hello World")
    .titleStyle() 
    
    
// Custom Containers, for example a new type of stack called a GridStack

struct GridStack<Content: View>: View {
    let rows: Int
    let columns: Int
    @ViewBuilder let content: (Int, Int) -> Content

    var body: some View {
        VStack {
            ForEach(0..<rows, id:\.self) { row in
                HStack {
                    ForEach(0..<columns, id: \.self) { column in
                        content(row, column)
                    }
                }
            }
        }
    }
}

struct ContentView: View {
    var body: some View {
        GridStack(rows: 4, columns: 4) { row, col in
            Image(systemName: "\(row * 4 + col).circle")
            Text("R\(row) C\(col)")
        }
    }
}


```


