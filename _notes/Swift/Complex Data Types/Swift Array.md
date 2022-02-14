---
title: Swift Array
---

### Main Idea

A complex data type that holds a multiple pieces of data in one place. Arrays can be of different data types, Strings, Int, and Float. An array can be of a single data type, Arrays are typesafe.

```swift

// Create a specialize array type without a value
var albums = Array<String>()
albums.append("Folklore")
albums.append("Fearless")
albums.append("Red")

var albums = [String]()
albums.append("Folklore")
albums.append("Fearless")
albums.append("Red")


// We can use .count
print(albums.count)

// We can remove(at:) and removeAll()
var characters = ["Lana", "Pam", "Ray", "Sterling"]
print(characters.count)

characters.remove(at: 2)
print(characters.count)

characters.removeAll()
print(characters.count)


// We can check if  array contains a particular item with contains()
let bondMovies = ["Casino Royale", "Spectre", "No Time To Die"]
print(bondMovies.contains("Frozen"))

// We can sort an array with sorted()
let cities = ["London", "Tokyo", "Rome", "Budapest"]
print(cities.sorted())

// We can reverse an array with .reversed()
let presidents = ["Bush", "Obama", "Trump", "Biden"]
let reversedPresidents = presidents.reversed()
print(reversedPresidents)
```
