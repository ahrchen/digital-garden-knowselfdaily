---
title: Swift Comparable Protocols
---

### Main Idea

We can make our own types conform to Comparable, and when we do so we also get a sorted() method with no parameters. This takes two steps:

1. Add the Comparable conformance to the definition of User.
2. Add a method called < that takes two users and returns true if the first should be sorted before the second.

```swift
struct User: Identifiable, Comparable {
    let id = UUID()
    let firstName: String
    let lastName: String
    
    static func <(lhs:User, rhs:User) -> Bool {
        lhs.lastName < rhs.lastName
    }
}

struct ContentView: View {
    let users = [
        User(firstName: "Arnold", lastName: "Rimmer"),
        User(firstName: "Kristine", lastName: "Kochanski"),
        User(firstName: "David", lastName: "Lister")
    ].sorted()
    
    var body: some View {
        List(users) { user in
            Text("\(user.lastName), \(user.firstName)")
        }
    }
}
```

