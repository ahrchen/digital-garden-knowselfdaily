---
title: Swift Closures
---

### Main Idea
Closures are a bit like anonymous functions - functions we can create and assign directly to a variable or pass into other functions to customize how they work. Passing one function into another as a parameter.

One of the most common reasons for closures in Swift is to store functionality – to be able to say “here’s some work I want you to do at some point, but not necessarily now.” Some examples:

1. Running some code after a delay.
2. Running some code after an animation has finished.
3. Running some code when a download has finished.
4. Running some code when a user has selected an option from your menu.


Example Usecases
1. When you create a list of data on the screen, SwiftUI will ask you to provide a function that accepts one item from the list and converts it something it can display on-screen.
2. When you create a button, SwiftUI will ask you to provide one function to execute when the button is pressed, and another to generate the contents of the button – a picture, or some text, and so on.
3. Even just putting stacking pieces of text vertically is done using a closure.
```swift
// Copy function into variable
func greetUser() {
    print("Hi there!")
}

greetUser()

var greetCopy = greetUser
greetCopy()

// Assign function into variable
let sayHello = {
    print("Hi there!")
}

sayHello()

// Add parameter to closure
let sayHello = { (name: String) -> String in
    "Hi \(name)!"
}

sayHello("Taylor")

// Type Annotation for Closures
var greetCopy: () -> Void = greetUser

// We lose the name of the variable
func getUserData(for id: Int) -> String {
    if id == 1989 {
        return "Taylor Swift"
    } else {
        return "Anonymous"
    }
}

let data: (Int) -> String = getUserData
let user = data(1989)
print(user)


let team = ["Gloria", "Suzanne", "Piper", "Tiffany", "Tasha"]
let sortedTeam = team.sorted()
print(sortedTeam)

func captainFirstSorted(name1: String, name2: String) -> Bool {
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
}

let captainFirstTeam = team.sorted(by: captainFirstSorted)
print(captainFirstTeam)

// pass entire closure into the function
let captainFirstTeam = team.sorted(by: { (name1: String, name2: String) -> Bool in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
}

// Trailing Closures and shorthand syntax

// Remove the by: and closing paranthesis and typing string, string -> bool already known
let captainFirstTeam = team.sorted { name1, name2 in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
}

// Shorthand $0 and $1 to remove name1 and name2
let captainFirstTeam = team.sorted {
    if $0 == "Suzanne" {
        return true
    } else if $1 == "Suzanne" {
        return false
    }

    return $0 < $1
}

// If you use simple code like reverse sort you can use 
let reverseTeam = team.sorted {
    return $0 > $1
}

// Usecases

let tOnly = team.filter { $0.hasPrefix("T") }
print(tOnly)

let uppercaseTeam = team.map { $0.uppercased() }
print(uppercaseTeam)

// Write functions that accept functions as parameters

func makeArray(size: Int, using generator: () -> Int) -> [Int] {
    var numbers = [Int]()

    for _ in 0..<size {
        let newNumber = generator()
        numbers.append(newNumber)
    }

    return numbers
}

let rolls = makeArray(size: 50) {
    Int.random(in: 1...20)
}

print(rolls)

// Dedictated functions work too
func generateNumber() -> Int {
    Int.random(in: 1...20)
}

let newRolls = makeArray(size: 50, using: generateNumber)
print(newRolls)

// Multiple trailing closures
func doImportantWork(first: () -> Void, second: () -> Void, third: () -> Void) {
    print("About to start first work")
    first()
    print("About to start second work")
    second()
    print("About to start third work")
    third()
    print("Done!")
}

doImportantWork {
    print("This is the first work")
} second: {
    print("This is the second work")
} third: {
    print("This is the third work")
}
```


