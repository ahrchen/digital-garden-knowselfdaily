---
title: Swift Enum
---

### Main Idea

A complex data type that holds multiple pieces of data more efficiently and safely. By forcing people to select between a few options. 

```swift

enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
}

// Force day cannot be anything else
var day = Weekday.monday
day = Weekday.tuesday
day = Weekday.friday

// Quick Enum
enum Weekday {
    case monday, tuesday, wednesday, thursday, friday
}

// Skip the type because we already know the data type
var day = Weekday.monday
day = .tuesday
day = .friday

// Much more safe and efficient to store 
M, o, n, d, a, y than Weekday.monday which is 0. 
```
