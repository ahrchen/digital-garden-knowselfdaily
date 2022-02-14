---
title: Swift String
---

### Main Idea

A basic data type that holds a string of character at time.

```swift

Escape character \ backslash
let quote = "Then he tapped a sign saying \"Believe\" and walked away."

// Multiline 
Let movie = “””
A day in
The life of an
Apple engineer
“””

// Number of characters
print(actor.count)

// Uppercase
print(actor.uppercased())

// HasPrefix() - Starts with a string
print(movie.hasPrefix(“A day”))

// HasSuffix() - Ends with a string
print(filename.hasSuffix(“.jpg”)

// String Interpolation
let name = "Taylor"
let age = 26
let message = "Hello, my name is \(name) and I'm \(age) years old."
print(message)

// This allows us to combine ints and strings quickly
let number = 11
// Nope
let missionMessage = "Apollo " + number + " landed on the moon."
// Doable
let missionMessage = "Apollo " + String(number) + " landed on the moon."
// Better
let missionMessage = "Apollo \(number) landed on the moon."

// How to join strings
let firstPart = "Hello, "
let secondPart = "world!"
let greeting = firstPart + secondPart

// + -> Operator Overloading 

// Each + join each string one at a time
let luggageCode = "1" + "2" + "3" + "4" + "5"
// “12” + "3" + "4" + "5"
// “123" + "4" + "5"
// “1234” + "5"
// “12345"

// separate a string in to array
let input = "a b c"
let letters = input.components(separatedBy: " ")
let letter = letters.randomElement()

// Trim

let trimmed = letter?.trimmingCharacters(in: .whitespacesAndNewlines)

// UITextChecker the ability to check for misspelled words. 
// -- 1. From UIKit
// -- 2. Written in Objective-C

let word = "swift"
let checker = UITextChecker()
// Use Objc-C text range 
let range = NSRange(location: 0, length: word.utf16.count)
// Check the string at a range
let misspelledRange = checker.rangeOfMisspelledWord(in: word, range: range, startingAt: 0, wrap: false, language: "en")
// No Misspelling found is NSNotFound
let allGood = misspelledRange.location == NSNotFound
```
