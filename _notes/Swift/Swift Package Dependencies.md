---
title: Swift Package Dependencies
---

### Main Idea

We use package dependencies to solve problem that are too risky or complex. Using the Swift Package Manager we can download dependency. 
```swift
import SamplePackage
import SwiftUI

struct ContentView: View {
    
    let possibleNumbers = Array(1...60)
    
    var results: String {
        let selected = possibleNumbers.random(7).sorted()
        let strings = selected.map(String.init)
        return strings.joined(separator: ", ")
    }
    var body: some View {
        Text(results)
    }
}
```
