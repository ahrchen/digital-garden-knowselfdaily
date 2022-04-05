---
title: SwiftUI Environment Wrapper
---

### Main Idea
 Well, @EnvironmentObject takes that one step further: we can place an object into the environment so that any child view can automatically have access to it.
 
 Imagine we had multiple views in an app, all lined up in a chain: view A shows view B, view B shows view C, C shows D, and D shows E. View A and E both want to access the same object, but to get from A to E you need to go through B, C, and D, and they don’t care about that object. If we were using @ObservedObject we’d need to pass our object from each view to the next until it finally reached view E where it could be used, which is annoying because B, C, and D don’t care about it. With @EnvironmentObject view A can put the object into the environment, view E can read the object out from the environment, and views B, C, and D don’t have to know anything happened – it’s much nicer.
 
 Now, you might wonder how SwiftUI makes the connection between .environmentObject(user) and @EnvironmentObject var user: User – how does it know to place that object into the correct property?
 
 Well, you’ve seen how dictionaries let us use one type for the key and another for the value. The environment effectively lets us use data types themselves for the key, and instances of the type as the value. This is a bit mind bending at first, but imagine it like this: the keys are things like Int, String, and Bool, with the values being things like 5, “Hello”, and true, which means we can say “give me the Int” and we’d get back 5.
 
 ### Usage
 
 ```swift
 @MainActor class User: ObservableObject {
    @Published var name = "Taylor Swift"
}

struct EditView: View {
    @EnvironmentObject var user: User
    
    var body: some View {
        TextField("Name", text: $user.name)
    }
}

struct DisplayView: View {
    @EnvironmentObject var user: User
    
    var body: some View {
        Text(user.name)
    }
}

struct ContentView: View {
    @StateObject var user: User
    
    init() {
        self._user = StateObject(wrappedValue: (User()))
    }
    
    var body: some View {
        VStack {
            EditView()
            DisplayView()
        }
        .environmentObject(user)
    }
}
```
 
 
 @Environment, and it allows us to create properties that store values provided to us externally. Is the user in light mode or dark mode? Have they asked for smaller or larger fonts? What timezone are they on? All these and more are values that come from the environment, and in this instance we’re going to ask the environment to dismiss our view.


### Usage

```swift
struct SecondView: View {
    @Environment(\.dismiss) var dismiss
    let name: String
    
    var body: some View {
        Button("Dismiss") {
            dismiss()
        }
    }
}

struct ContentView: View {
    @State private var showingSheet = false
    
    var body: some View {
        Button("Show Sheet") {
            showingSheet.toggle()
        }
        .sheet(isPresented: $showingSheet) {
            SecondView(name: "@two")
        }
    }
}
```
