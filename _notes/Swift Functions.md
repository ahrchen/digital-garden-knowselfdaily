---
title: Swift Functions
---

### Main Idea

Functions let us wrap up pieces of code so they can be used in lots of places. We can send data into functions to customize how they work, and get back data that tells us the result that was calculated.


```swift

// Use functions when you plan to reuse the code again and again. 
// 1. Benefit: One change changes the code everywhere the code is used.
// 2. Benefit: Break up code to follow more easily
// 3. Benefit: Function composition. 

func showWelcome() {
    print("Welcome to my app!")
    print("By default This prints out a conversion")
    print("chart from centimeters to inches, but you")
    print("can also set a custom range if you want.")
}

showWelcome() // Callsite

// Use parameters number: Int
a
func printTimesTables(number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(number: 5)

// Return data

 func rollDice() -> Int {
    return Int.random(in: 1...6)
}

let result = rollDice()
print(result)


// return is not necessary when it is oneline

 func rollDice() -> Int {
    Int.random(in: 1...6)
}


func pythagoras(a: Double, b: Double) -> Double {
    let input = a * a + b * b
    let root = sqrt(input)
    return root
}

let c = pythagoras(a: 3, b: 4)
print(c)

func pythagoras(a: Double, b: Double) -> Double {
    sqrt(a * a + b * b)
}

// return multiple values

// Use Array
func getUser() -> [String] {
    ["Taylor", "Swift"]
}

let user = getUser()
print("Name: \(user[0]) \(user[1])") 

// Use Dictionary
func getUser() -> [String: String] {
    [
        "firstName": "Taylor",
        "lastName": "Swift"
    ]
}

let user = getUser()
print("Name: \(user["firstName", default: "Anonymous"]) \(user["lastName", default: "Anonymous"])") 

// Use Tuple, know exact type and value while dictionary doesn't know
func getUser() -> (firstName: String, lastName: String) {
    (firstName: "Taylor", lastName: "Swift")
}

let user = getUser()
print("Name: \(user.firstName) \(user.lastName)")

let (firstName, lastName) = getUser()
print("Name: \(firstName) \(lastName)")

let (firstName, _) = getUser()
print("Name: \(firstName)")

// Simplfy
func getUser() -> (firstName: String, lastName: String) {
    ("Taylor", "Swift")
}

func getUser() -> (String, String) {
    ("Taylor", "Swift")
}

let user = getUser()
print("Name: \(user.0) \(user.1)")

// Naming Parameters

func rollDice(sides: Int, count: Int) -> [Int] {
    // Start with an empty array
    var rolls = [Int]()

    // Roll as many dice as needed
    for _ in 1...count {
        // Add each result to our array
        let roll = Int.random(in: 1...sides)
        rolls.append(roll)
    }

    // Send back all the rolls
    return rolls
}

let rolls = rollDice(sides: 6, count: 4)

// The parameter determine the name
func hireEmployee(name: String) { }
func hireEmployee(title: String) { }
func hireEmployee(location: String) { }

// Use _ to ignore the parameter name 
// BEFORE
func isUppercase(string: String) -> Bool {
    string == string.uppercased()
}

let string = "HELLO, WORLD"
let result = isUppercase(string: string)
// AFTER
func isUppercase(_ string: String) -> Bool {
    string == string.uppercased()
}

let string = "HELLO, WORLD"
let result = isUppercase(string)

// Custom external parameter naming
// BEFORE
func printTimesTables(number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(number: 5)
// AFTER
func printTimesTables(for number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(for: 5)

// Provide default values for parameters
// Shorter, simpler code most of the time, but flexibility when we need it – perfect.
// simplify complex function, and make your code easier to write.

func printTimesTables(for number: Int, end: Int = 12) {
    for i in 1...end {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(for: 5, end: 20)
printTimesTables(for: 8)

var characters = ["Lana", "Pam", "Ray", "Sterling"]
print(characters.count)
characters.removeAll()
print(characters.count)

characters.removeAll(keepingCapacity: true)

// Handle Errors in functions
// 
enum PasswordError: Error {
    case short, obvious
}

func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    }

    if password == "12345" {
        throw PasswordError.obvious
    }

    if password.count < 8 {
        return "OK"
    } else if password.count < 10 {
        return "Good"
    } else {
        return "Excellent"
    }
}

let string = "12345"


do {
    let result = try checkPassword(string)
    print("Password rating: \(result)")
} catch PasswordError.short {
    print("Please use a longer password.")
} catch PasswordError.obvious {
    print("I have the same combination on my luggage!")
} catch {
    print("There was an error.")
}

// do try catch, by forcing us to use try before every throwing function, we’re explicitly acknowledging which parts of our code can cause errors.
do {
    try throwingFunction1()
    nonThrowingFunction1()
    try throwingFunction2()
    nonThrowingFunction2()
    try throwingFunction3()
} catch {
    // handle errors
}
```
