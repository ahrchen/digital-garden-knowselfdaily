---
title: Swift Tabs
---

### Main Idea

We use Tabs to let the user pick between multiple views 

```swift
struct ContentView: View {

    @State private var selectedTab = "One"
    
    var body: some View {
        TabView(selection: $selectedTab) {
            Text("Tab 1")
                .onTapGesture {
                    self.selectedTab = "Two"
                }
                .tabItem {
                    Image(systemName: "star")
                    Text("One")
                }
                .tag("One")
            
            Text("Tab 2")
                .onTapGesture {
                    self.selectedTab = "One"
                }
                .tabItem {
                    Image(systemName: "star.fill")
                    Text("Two")
                }
                .tag("Two")
        }
    }
}
```
