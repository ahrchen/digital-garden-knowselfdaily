---
title: SwiftUI Property Wrappers
---

### Main Idea

An attribute placed around a property that gives it custom abilities. For example, you could write a @UserDefaults property wrapper to make loading and saving data to user defaults easier. 

Property wrappers have that name because they wrap our property inside another struct. What this means is that when we use @State to wrap a string, the actual type of property we end up with is a State<String>. Similarly, when we use @Environment and others we end up with a struct of type Environment that contains some other value inside it.

#### Topics
- [[SwiftUI State Wrapper]]
- [[SwiftUI Binding]]
- [[SwiftUI ObservedObject Wrapper]]
- [[SwiftUI ObservableObject Wrapper]]
- [[SwiftUI FetchRequest Wrapper]]
- [[SwiftUI FocusState Wrapper]] 
- [[SwiftUI StateObject Wrapper]]
- [[SwiftUI Environment Wrapper]]
- [[SwiftUI MainActor Wrapper]]
- [[SwiftUI ViewBuilder Wrapper]]
