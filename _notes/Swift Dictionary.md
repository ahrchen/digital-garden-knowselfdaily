---
title: Swift Dictionary
---

### Main Idea

A complex data type that holds multiple values using a key and value. We need a dictionary when arrays does not function for our purpose of finding a value for a key. 

```swift

// Why we need dictionaries?

var employee = ["Taylor Swift", "Singer", "Nashville"]

print("Name: \(employee[0])")
print("Job title: \(employee[1])")
print("Location: \(employee[2])")

print("Name: \(employee[0])")
employee.remove(at: 1)
print("Job title: \(employee[1])")
print("Location: \(employee[2])")    

// Better to be explicit
let employee2 = ["name": "Taylor Swift", "job": "Singer", "location": "Nashville"]

let employee2 = [
    "name": "Taylor Swift",
    "job": "Singer", 
    "location": "Nashville"
]

// If you print you will get many Optionals to keep keys safe. 
print(employee2["password"])
print(employee2["status"])
print(employee2["manager"])

// Try instead add a default value 

print(employee2["name", default: "Unknown"])
print(employee2["job", default: "Unknown"])
print(employee2["location", default: "Unknown"])

// Use explict types you want to store
var heights = [String: Int]()
heights["Yao Ming"] = 229
heights["Shaquille O'Neal"] = 216
heights["LeBron James"] = 206

// We cannot have duplicate keys, we will overwrite a key
var archEnemies = [String: String]()
archEnemies["Batman"] = "The Joker"
archEnemies["Superman"] = "Lex Luthor"
archEnemies["Batman"] = "Penguin"
```
