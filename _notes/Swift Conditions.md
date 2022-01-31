---
title: Swift Conditions
---

### Main Idea
Conditions let us evaluate our program’s state as it runs and take different action depending on the result, using operators and conditions.


```swift

// if someCondition {
//    print("Do Somthing")
// }

// comparison operator --> >, <, ==, !=  
let speed = 88
let percentage = 85
let age = 18

if speed >= 88 {
    print("Where we're going we don't need roads.")
}

if percentage < 85 {
    print("Sorry, you failed the test.")
}

if age >= 18 {
    print("You're eligible to vote")
}

// These are the same
// Create the username variable
var username = "taylorswift13"

// If `username` contains an empty string
if username == "" {
    // Make it equal to "Anonymous"
    username = "Anonymous"
}

// Now print a welcome message
print("Welcome, \(username)!")

// inefficent because counting string
if username.count == 0 {
    username = "Anonymous"
}

// much faster
if username.isEmpty == true {
    username = "Anonymous"
}

// cleaner
if username.isEmpty {
    username = "Anonymous"
}

// Enums compare by the case that comes first
enum Sizes: Comparable {
    case small
    case medium
    case large
}

let first = Sizes.small
let second = Sizes.large
print(first < second) // True

// Multiple Conditions
if someCondition {
    print("This will run if the condition is true")
} else {
    print("This will run if the condition is false")
}

let a = false
let b = true

if a {
    print("Code to run if a is true")
} else if b {
    print("Code to run if a is false but b is true")
} else {
    print("Code to run if both a and b are false")
}

These are the same
if temp > 20 {
    if temp < 30 {
        print("It's a nice day.")
    }
}

//Logical Operator && and || 
if temp > 20 && temp < 30 {
    print("It's a nice day.")
}

let userAge = 14
let hasParentalConsent = true

if userAge >= 18 || hasParentalConsent == true {
    print("You can buy the game")
}

// When to use else if

// BEFORE
if score > 9000 {
    print("It's over 9000!")
} else {
    if score == 9000 {
        print("It's exactly 9000!")
    } else {
        print("It's not over 9000!")
    }
}

// AFTER
if score > 9000 {
    print("It's over 9000!")
} else if score == 9000 {
    print("It's exactly 9000!")
} else {
    print("It's not over 9000!")
}

// When to use Switch

// BEFORE
enum Weather {
    case sun, rain, wind, snow, unknown
}

let forecast = Weather.sun

if forecast == .sun {
    print("It should be a nice day.")
} else if forecast == .rain {
    print("Pack an umbrella.")
} else if forecast == .wind {
    print("Wear something warm")
} else if forecast == .rain {
    print("School is cancelled.")
} else {
    print("Our forecast generator is broken!")
}

// PROBLEMS
// 1. repeat forecast
// 2. rain checked twice
// 3. did not check snow

// FIX Switch with mutually exclusive
// Only run the first match

// AFTER 
switch forecast {
case .sun:
    print("It should be a nice day.")
case .rain:
    print("Pack an umbrella.")
case .wind:
    print("Wear something warm")
case .snow:
    print("School is cancelled.")
case .unknown:
    print("Our forecast generator is broken!")
}

// Use default for strings and ints 
let place = "Metropolis"

switch place {
case "Gotham":
    print("You're Batman!")
case "Mega-City One":
    print("You're Judge Dredd!")
case "Wakanda":
    print("You're Black Panther!")
default:
    print("Who are you?")
}

let day = 5
print("My true love gave to me…")

switch day {
case 5:
    print("5 golden rings")
case 4:
    print("4 calling birds")
case 3:
    print("3 French hens")
case 2:
    print("2 turtle doves")
default:
    print("A partridge in a pear tree")
}

// Use fallthrough to run next case below
let day = 5
print("My true love gave to me…")

switch day {
case 5:
    print("5 golden rings")
    fallthrough
case 4:
    print("4 calling birds")
    fallthrough
case 3:
    print("3 French hens")
    fallthrough
case 2:
    print("2 turtle doves")
    fallthrough
default:
    print("A partridge in a pear tree")
}

// Use ternary for quick checks
let age = 18
let canVote = age >= 18 ? "Yes" : "No"
canVote is "Yes"

let hour = 23
print(hour < 12 ? "It's before noon" : "It's after noon")
         WHAT           TRUE                FALSE
let names = ["Jayne", "Kaylee", "Mal"]   
let crewCount = names.isEmpty ? "No one" : "\(names.count) people"
print(crewCount)


enum Theme {
    case light, dark
}

let theme = Theme.dark

let background = theme == .dark ? "black" : "white"
print(background)


// WHEN TO USE TERNARY
if hour < 12 {
    print("It's before noon")
} else {
    print("It's after noon")
}

let hour = 23
print(hour < 12 ? "It's before noon" : "It's after noon")
```


