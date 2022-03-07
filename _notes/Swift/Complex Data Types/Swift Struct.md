---
title: Swift Struct
---

### Main Idea
Structs are one of the ways Swift lets us create our own data types out of several small types. For example, you might put three strings and a Boolean together and say that represents a user in your app. In fact, most of Swift’s own types are implemented as structs, including String, Int, Bool, Array, and more.

####Methods vs Functions

1. The only real difference is that methods belong to a type, such as structs, enums, and classes, whereas functions do not. That’s it – that’s the only difference. Both can accept any number of parameters, including variadic parameters, and both can return values. Heck, they are so similar that Swift still uses the func keyword to define a method. 


2. Of course, being associated with a specific type such as a struct means that methods gain one important super power: they can refer to the other properties and methods inside that type, meaning that you can write a describe() method for a User type that prints the user’s name, age, and city. 

3. There is one more advantage to methods, but it’s quite subtle: methods avoid namespace pollution. Whenever we create a function, the name of that function starts to have meaning in our code – we can write wakeUp() and have it do something. So, if you write 100 functions you end up with 100 reserved names, and if you write 1000 functions you have 1000 reserved names. That can get messy quickly, but by putting functionality into methods we restrict where those names are available – wakeUp() isn’t a reserved name any more unless we specifically write someUser.wakeUp(). This reduces the so-called pollution, because if most of our code is in methods then we won’t get name clashes by accident.





```swift
struct Album {
    let title: String
    let artist: String
    let year: Int

    func printSummary() {
        print("\(title) (\(year)) by \(artist)")
    }
}

// At this point, Album is just like String or Int – we can make them, assign values, copy them, and so on.
let red = Album(title: "Red", artist: "Taylor Swift", year: 2012)
let wings = Album(title: "Wings", artist: "BTS", year: 2016)

print(red.title)
print(wings.artist)

red.printSummary()
wings.printSummary()

// Structs with values that can change
struct Employee {
    let name: String
    var vacationRemaining: Int

    mutating func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
            print("I'm going on vacation!")
            print("Days remaining: \(vacationRemaining)")
        } else {
            print("Oops! There aren't enough days remaining.")
        }
    }
}

var archer = Employee(name: "Sterling Archer", vacationRemaining: 14)
archer.takeVacation(days: 5)
print(archer.vacationRemaining)

// However we cannot call takeVacation on a constant, the following will fail
let archer = Employee(name: "Sterling Archer", vacationRemaining: 14) 

// This is a little bit of what’s called syntactic sugar – Swift silently creates a special function inside the struct called init(), using all the properties of the struct as its parameters. It then automatically treats these two pieces of code as being the same:

var archer1 = Employee(name: "Sterling Archer", vacationRemaining: 14)
var archer2 = Employee.init(name: "Sterling Archer", vacationRemaining: 14)


// Now you can see what’s really happening here: Swift’s own Double type is implemented as a struct, and has an initializer function that accepts an integer.
let a = 1
let b = 2.0
let c = Double(a) + b

// Set default variables. If you assign a default value to a constant property, that will be removed from the initializer entirely.  To assign a default but leave open the possibility of overriding it when needed, use a variable property.
let name: String
var vacationRemaining = 14
let kane = Employee(name: "Lana Kane")
let poovey = Employee(name: "Pam Poovey", vacationRemaining: 35)

// Computed Properties, are a blend of both stored properties and functions: they are accessed like stored properties, but work like functions. if you regularly read the property when its value hasn’t changed, then using a stored property will be much faster than using a computed property. On the other hand, if your property is read very rarely and perhaps not at all, then using a computed property saves you from having to calculate its value and store it somewhere. When it comes to dependencies – whether your property’s value relies on the values of your other properties – then the tables are turned: this is a place where computed properties are useful, because you can be sure the value they return always takes into account the latest program state.
struct Employee {
    let name: String
    var vacationAllocated = 14
    var vacationTaken = 0

    var vacationRemaining: Int {
        vacationAllocated - vacationTaken
    }
}

var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
archer.vacationTaken += 4
print(archer.vacationRemaining)
archer.vacationTaken += 4
print(archer.vacationRemaining)

// To write to the property we need a setter and getter to read
var vacationRemaining: Int {
    get {
        vacationAllocated - vacationTaken
    }

    set {
        vacationAllocated = vacationTaken + newValue
    }
}

var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
archer.vacationTaken += 4
archer.vacationRemaining = 5
print(archer.vacationAllocated)

// Property observers to take action when a property changes. These take two forms: a didSet observer to run when the property just changed, and a willSet observer to run before the property changed. The most important reason is convenience: using a property observer means your functionality will be executed whenever the property changes. Sure, you could use a function to do that, but would you remember? Always? In every place you change the property? Most of the time we use didSet to take action after the change has happened so that we can update our user interface, save changes, or whatever. Sometimes willSet is used is when you need to know the state of your program before a change is made. For example, SwiftUI uses willSet in some places to handle animations so that it can take a snapshot of the user interface before a change. When it has both the “before” and “after” snapshot, it can compare the two to see all the parts of the user interface that need to be updated.

struct Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var game = Game()
game.score += 10
game.score -= 3
game.score += 1


struct App {
    var contacts = [String]() {
        willSet {
            print("Current value is: \(contacts)")
            print("New value will be: \(newValue)")
        }

        didSet {
            print("There are now \(contacts.count) contacts.")
            print("Old value was \(oldValue)")
        }
    }
}

var app = App()
app.contacts.append("Adrian E")
app.contacts.append("Allen W")
app.contacts.append("Ish S")

// Create custom initializers
struct Player {
    let name: String
    let number: Int

    init(name: String, number: Int) {
        self.name = name
        self.number = number
    }
    
    init(name: String) {
        self.name = name
        number = Int.random(in: 1...99)
    }
}

// limit access to internal data using access control
// Use private for “don’t let anything outside the struct use this.”
// Use fileprivate for “don’t let anything outside the current file use this.”
// Use public for “let anyone, anywhere use this.”
// private(set) “let anyone read this property, but only let my methods write it.” 
struct BankAccount {
    private(set) var funds = 0

    mutating func deposit(amount: Int) {
        funds += amount
    }

    mutating func withdraw(amount: Int) -> Bool {
        if funds > amount {
            funds -= amount
            return true
        } else {
            return false
        }
    }
}

if success {
    print("Withdrew money successfully")
} else {
    print("Failed to get the money")
} 

// Static properties and methods,  I use this technique a lot with SwiftUI for two things: creating example data, and storing fixed data that needs to be accessed in various places.

// Notice the keyword static in there, which is what means both the studentCount and add() methods belong to the School struct itself rather than to individual instances of the struct.

struct School {
    static var studentCount = 0

    static func add(student: String) {
        print("\(student) joined the school.")
        studentCount += 1
    }
}

School.add(student: "Taylor Swift")
print(School.studentCount)


// If you want to mix and match static and non-static properties and methods, there are two rules:

// 1. To access non-static code from static code… you’re out of luck: static properties and methods can’t refer to non-static properties and methods because it just doesn’t make sense – which instance of School would you be referring to?
// 2. To access static code from non-static code, always use your type’s name such as School.studentCount. You can also use Self to refer to the current type.
// Now we have self and Self, and they mean different things: self refers to the current value of the struct, and Self refers to the current type.

//Examples 

// Organize common data in my apps
struct AppData {
    static let version = "1.3 beta 2"
    static let saveFilename = "settings.json"
    static let homeURL = "https://www.hackingwithswift.com"
}
AppData.version

// Store example data for preview screen 
struct Employee {
    let username: String
    let password: String

    static let example = Employee(username: "cfederighi", password: "hairforceone")
}
Employee.example 

// TIPS

// Choose Struct over Tuples if you plan to use the data type multiple times, because you keep the data type in a single spot for editing
func authenticate(_ user: User) { ... }
func showProfile(for user: User) { ... }
func signOut(_ user: User) { ... }
// vs
func authenticate(_ user: (name: String, age: Int, city: String)) { ... }
func showProfile(for user: (name: String, age: Int, city: String)) { ... }
func signOut(_ user: (name: String, age: Int, city: String)) { ... }


// Keep Memberwise initialize by moving custom initilaizer to extension 
struct Employee {
    var name: String
    var yearsActive = 0
}

extension Employee {
    init() {
        self.name = "Anonymous"
        print("Creating an anonymous employee…")
    }
}


```


