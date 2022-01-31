---
title: Swift Type Annotation
---

### Main Idea

A type annotations let us be explicit about what data type we want for a variable or constant.

When to use type annotations
The answer to the first question is primarily one of three reasons:

1. Swift can’t figure out what type should be used.
2. You want Swift to use a different type from its default.
3. You don’t want to assign a value just yet.

```swift

//String holds text:

let playerName: String = "Roy"
//Int holds whole numbers:

var luckyNumber: Int = 13
//Double holds decimal numbers:

let pi: Double = 3.141
//Bool holds either true or false:

var isAuthenticated: Bool = true
//Array holds lots of different values, all in the order you add them. This must be specialized, such as [String]:

var albums: [String] = ["Red", "Fearless"]
//Dictionary holds lots of different values, where you get to decide how data should be accessed. This must be specialized, such as [String: Int]:

var user: [String: String] = ["id": "@twostraws"]
// Set holds lots of different values, but stores them in an order that’s optimized for checking what it contains. This must be specialized, such as Set<String>:

var books: Set<String> = Set(["The Bluest Eye", "Foundation", "Girl, Woman, Other"])

// Values of an enum have the same type as the enum itself, so we could write something like this:
enum UIStyle {
    case light, dark, system
}

var style = UIStyle.light
style = .dark

// When to use type annotation? Constants I don’t have a value for yet. You see, Swift is really clever: you can create a constant that doesn’t have a value just yet, later on provide that value, and Swift will ensure we don’t accidentally use it until a value is present. It will also ensure that you only ever set the value once, so that it remains constant.

// For example:

let username: String
// lots of complex logic
username = "@knowselfdaily"
// lots more complex logic
print(username)
```
