---
title: Swift Package Dependencies
---

### Main Idea

We use package dependencies to solve problem that are too risky or complex. Using the Swift Package Manager we can download dependency. 

The reason this is possible is because most developers have agreed a system of semantic versioning (SemVer) for their code. If you look at a version like 1.5.3, then the 1 is considered the major number, the 5 is considered the minor number, and the 3 is considered the patch number. If developers follow SemVer correctly, then they should:

1. Change the patch number when fixing a bug as long as it doesn’t break any APIs or add features.
2. Change the minor number when they added features that don’t break any APIs.
3. Change the major number when they do break APIs.

Anyway, the first step is to add the package to our project: go to the File menu and choose Add Packages. For the URL enter https://github.com/twostraws/SamplePackage, which is where the code for my example package is stored. Xcode will fetch the package, read its configuration, and show you options asking which version you want to use. The default will be “Version – Up to Next Major”, which is the most common one to use and means if the author of the package updates it in the future then as long as they don’t introduce breaking changes Xcode will update the package to use the new versions.

PS: You can read the source code for my simple extension right inside Xcode – just open the Sources > SamplePackage group and look for SamplePackage.swift. You’ll see it doesn’t do much!

Reference - https://www.hackingwithswift.com/books/ios-swiftui/adding-swift-package-dependencies-in-xcode
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
