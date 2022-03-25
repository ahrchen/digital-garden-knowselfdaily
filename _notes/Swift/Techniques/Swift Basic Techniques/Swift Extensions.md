---
title: Swift Extensions
---

### Main Idea
Extensions let us add functionality to any type, whether we created it or someone else created it – even one of Apple’s own types.

Extensions are also useful for organizing our own code, and although there are several ways of doing this I want to focus on two here: conformance grouping and purpose grouping.

Conformance grouping means adding a protocol conformance to a type as an extension, adding all the required methods inside that extension. This makes it easier to understand how much code a developer needs to keep in their head while reading an extension – if the current extension adds support for Printable, they won’t find printing methods mixed in with methods from other, unrelated protocols.

On the other hand, purpose grouping means creating extensions to do specific tasks, which makes it easier to work with large types. For example, you might have an extension specifically to handle loading and saving of that type.
```swift

var quote = "   The truth is rarely pure and never simple   "
let trimmed = quote.trimmingCharacters(in: .whitespacesAndNewlines)

extension String {
    func trimmed() -> String {
        self.trimmingCharacters(in: .whitespacesAndNewlines)
    }
}

let trimmed = quote.trimmed()

// Equalivilent to 
func trim(_ string: String) -> String {
    string.trimmingCharacters(in: .whitespacesAndNewlines)
}
let trimmed2 = trim(quote)

// However the extension has a number of benefits over the global function, including:
// 1. When you type quote. Xcode brings up a list of methods on the string, including all the ones we add in extensions. This makes our extra functionality easy to find.
// 2. Writing global functions makes your code rather messy – they are hard to organize and hard to keep track of. On the other hand, extensions are naturally grouped by the data type they are extending.
// 3. Because your extension methods are a full part of the original type, they get full access to the type’s internal data. That means they can use properties and methods marked with private access control, for example.

// What’s more, extensions make it easier to modify values in place – i.e., to change a value directly, rather than return a new value.

mutating func trim() {
    self = self.trimmed()
}
quote.trim()

// You can also use extensions to add properties to types, but there is one rule: they must only be computed properties, not stored properties. The reason for this is that adding new stored properties would affect the actual size of the data types – if we added a bunch of stored properties to an integer then every integer everywhere would need to take up more space in memory, which would cause all sorts of problems.
var lines: [String] {
    self.components(separatedBy: .newlines)
}

// TIPS keep memberwise initializer in struct and create custom initializer 

struct Book {
    let title: String
    let pageCount: Int
    let readingHours: Int
}

let lotr = Book(title: "Lord of the Rings", pageCount: 1178, readingHours: 24)

extension Book {
    init(title: String, pageCount: Int) {
        self.title = title
        self.pageCount = pageCount
        self.readingHours = pageCount / 50
    }
}

// Example 

let guests = ["Mario", "Luigi", "Peach"]

// This NO
if guests.isEmpty == false {
    print("Guest count: \(guests.count)")
}

// This NO
if !guests.isEmpty {
    print("Guest count: \(guests.count)")
}

// Try This
extension Array {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}

if guests.isNotEmpty {
    print("Guest count: \(guests.count)")
}

// How about Set, Dict, and Array
extension Collection {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}

// Extend this to the entire project protocol-oriented programming – we can list some required methods in a protocol, then add default implementations of those inside a protocol extension. 

// Example 1
protocol Person {
    var name: String { get }
    func sayHello()
}

extension Person {
    func sayHello() {
        print("Hi, I'm \(name)")
    }
}

struct Employee: Person {
    let name: String
}

let taylor = Employee(name: "Taylor Swift")
taylor.sayHello()

// Example 2

let numbers = [4, 8, 15, 16]
let allEven = numbers.allSatisfy { $0.isMultiple(of: 2) }


let numbers2 = Set([4, 8, 15, 16])
let allEven2 = numbers2.allSatisfy { $0.isMultiple(of: 2) }

let numbers3 = ["four": 4, "eight": 8, "fifteen": 15, "sixteen": 16]
let allEven3 = numbers3.allSatisfy { $0.value.isMultiple(of: 2) }

// Of course, the Swift developers don’t want to write this same code again and again, so they used a protocol extension: they wrote a single allSatisfy() method that works on a protocol called Sequence, which all arrays, sets, and dictionaries conform to. This meant the allSatisfy() method immediately became available on all those types, sharing exactly the same code.
```


