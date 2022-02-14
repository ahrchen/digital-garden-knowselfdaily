---
title: Swift Set
---

### Main Idea

A complex data type that holds multiple piece of data. No duplicates and no order

```swift

let people = Set(["Denzel Washington", "Tom Cruise", "Nicolas Cage", "Samuel L Jackson"])
print(people)

// explict 
var people = Set<String>()
people.insert("Denzel Washington")
people.insert("Tom Cruise")
people.insert("Nicolas Cage")
people.insert("Samuel L Jackson")

// .insert because we don't add on to the ordered list, it can go anywhere so insert

// .contains() is O(1) vs O(n) for arrays 
// .count get number of items
// .sorted() returns sorted array of set. 
```
