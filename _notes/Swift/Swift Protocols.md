---
title: Swift Protocols
---

### Main Idea
Protocols let us create blueprints of how our types share functionality, then use those blueprints in our functions to let them work on a wider variety of data. they let us define what kinds of functionality we expect a data type to support, and Swift ensures that the rest of our code follows those rules.s

```swift
func commute(distance: Int, using vehicle: Car) {
    // lots of code here
}

func commute(distance: Int, using vehicle: Train) {
    // lots of code here
}

func commute(distance: Int, using vehicle: Bus) {
    // lots of code here
}

protocol Vehicle {
    var name: String { get }
    var currentPassengers: Int { get set }
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}

// Conform to the Vehicle Protocol This means when you create new types that conform to the protocol you can add all sorts of other properties and methods as needed.

struct Car: Vehicle {
    let name = "Car"
    var currentPassengers = 1
    func estimateTime(for distance: Int) -> Int {
        distance / 50
    }

    func travel(distance: Int) {
        print("I'm driving \(distance)km.")
    }

    func openSunroof() {
        print("It's a nice day!")
    }
}

func commute(distance: Int, using vehicle: Car) {
    if vehicle.estimateTime(for: distance) > 100 {
        print("That's too slow! I'll try a different vehicle.")
    } else {
        vehicle.travel(distance: distance)
    }
}

let car = Car()
commute(distance: 100, using: car)

struct Bicycle: Vehicle {
    let name = "Bicycle"
    var currentPassengers = 1
    func estimateTime(for distance: Int) -> Int {
        distance / 10
    }

    func travel(distance: Int) {
        print("I'm cycling \(distance)km.")
    }
}

let bike = Bicycle()
commute(distance: 50, using: bike)

func getTravelEstimates(using vehicles: [Vehicle], distance: Int) {
    for vehicle in vehicles {
        let estimate = vehicle.estimateTime(for: distance)
        print("\(vehicle.name): \(estimate) hours to travel \(distance)km")
    }
}
getTravelEstimates(using: [car, bike], distance: 150)


// Opaque return type, so we can compute with similar protocol types 

func getRandomNumber() -> Int {
    Int.random(in: 1...6)
}

func getRandomBool() -> Bool {
    Bool.random()
}

// Attempt 
print(getRandomNumber() == getRandomNumber())
// -> Does not work

// Attempt 
func getRandomNumber() -> Equatable {
    Int.random(in: 1...6)
}

func getRandomBool() -> Equatable {
    Bool.random()
}
// -> Does not work



// --> Try this opaque return type using some, this means that swift knows what type it is, but we want to keep it open
func getRandomNumber() -> some Equatable {
    Int.random(in: 1...6)
}

func getRandomBool() -> some Equatable {
    Bool.random()
}
// This is where opaque return types come to the rescue: we can return the type some View, which means that some kind of view screen will be returned but we don’t want to have to write out its mile-long type. At the same time, Swift knows the real underlying type because that’s how opaque return types work: Swift always knows the exact type of data being sent back, and SwiftUI will use that create its layouts.
```


