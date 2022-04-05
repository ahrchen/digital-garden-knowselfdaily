---
title: SwiftUI Switch View with Enums
---

### Main Idea

Navigation views are great for letting us create hierarchical stacks of views that let users drill down into data, but they don’t work so well for showing unrelated data. For that we need to use SwiftUI’s TabView, which creates a button strip across the bottom of the screen, where tapping each button shows a different view.

Tip: It’s common to want to use NavigationView and TabView at the same time, but you should be careful: TabView should be the parent view, with the tabs inside it having a NavigationView as necessary, rather than the other way around.
### Usage

```swift
import SwiftUI

struct ContentView: View {
   @State private var selectedTab = "One"
    
    var body: some View {
        TabView(selection: $selectedTab) {
            Text("Tab 1")
                .onTapGesture {
                    selectedTab = "Two"
                }
                .tabItem {
                    Label("One", systemImage: "star")
                }
                .tag("One")
            
            Text("Tab 2")
                .onTapGesture {
                    selectedTab = "One"
                }
                .tabItem {
                    Label("Two", systemImage: "circle")
                }
                .tag("Two")
        }
        .onChange(of: selectedTab) { newValue in
            print("New value is \(newValue)")
        }
    }
}```
