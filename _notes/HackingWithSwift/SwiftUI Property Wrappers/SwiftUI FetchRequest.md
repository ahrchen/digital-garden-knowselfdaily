---
title: SwiftUI FetchRequest Wrapper
---

### Main Idea
 
SwiftUI gives us a dedicated property wrapper for working with Core Data fetch requests, and it allows us to embed data directly into SwiftUI views without having to write extra logic.

You must provide @FetchRequest with at least two values: the entity you want to read, and any sort descriptors to arrange the data. You can optionally also provide a predicate to filter the data as needed.

Important: Before using @FetchRequest you must first have injected a Core Data managed object context into the environment – see how to access a Core Data managed object context from a SwiftUI view for instructions on how to do that.


### Usage
```swift
@FetchRequest(
    entity: User.entity(),
    sortDescriptors: [
        NSSortDescriptor(keyPath: \User.name, ascending: false),
    ],
    predicate: NSPredicate(format: "surname == %@", "Hudson")
) var users: FetchedResults<User>
```
