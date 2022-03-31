---
title: SwiftUI Accessibility Hiding and Grouping Data
---

### Main Idea
SwiftUI Accessibility Hiding and Grouping, we can dictate what the voice reader will say using .accessibilityHidden and accessibilityElement() 

```swift
import SwiftUI
struct ContentView: View {
    
    var body: some View {
       Image(decorative: "character")
            .accessibilityHidden(true)
        
        VStack {
            Text("Your score is")
            Text("1000")
                .font(.title)
        }
        .accessibilityElement(children: .ignore) // same as .accessibilityElement()
        .accessibilityLabel("Your score is 1000")
    }
}
```

