---
title: Swift Class
---

### Main Idea
First, the things that classes and structs have in common include:

1. You get to create and name them.
2. You can add properties and methods, including property observers and access control.
3.You can create custom initializers to configure new instances however you want.

However, classes differ from structs in five key places:

1. You can make one class build upon functionality in another class, gaining all its properties and methods as a starting point. If you want to selectively override some methods, you can do that too.
2. Because of that first point, Swift won’t automatically generate a memberwise initializer for classes. This means you either need to write your own initializer, or assign default values to all your properties.
3. When you copy an instance of a class, both copies share the same data – if you change one copy, the other one also changes.
4. When the final copy of a class instance is destroyed, Swift can optionally run a special function called a deinitializer.
5. Even if you make a class constant, you can still change its properties as long as they are variables.


```swift
class Employee {
    let hours: Int

    init(hours: Int) {
        self.hours = hours
    }
    
    func printSummary() {
    print("I work \(hours) hours a day.")
}
}

// Use final to let other developers know how you will be using this class
final class Developer: Employee {
    func work() {
        print("I'm writing code for \(hours) hours.")
    }
    // if a child class wants to change a method from a parent class, you must use override in the child class’s version. This does two things:
    // 1. If you attempt to change a method without using override, Swift will refuse to build your code. This stops you accidentally overriding a method.
    // 2. If you use override but your method doesn’t actually override something from the parent class, Swift will refuse to build your code because you probably made a mistake.
    
    override func printSummary() {
        print("I'm a developer who will sometimes work \(hours) a day, but other times spend hours arguing about whether code should be indented using tabs or spaces.")
    }
}

class Manager: Employee {
    func work() {
        print("I'm going to meetings for \(hours) hours.")
    }
}

let robert = Developer(hours: 8)
let joseph = Manager(hours: 10)
robert.work()
joseph.work()
let novall = Developer(hours: 8)
novall.printSummary()


// Add initialize for classes 
// if a child class has any custom initializers, it must always call the parent’s initializer after it has finished setting up its own properties, if it has any.

class Vehicle {
    let isElectric: Bool

    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}

class Car: Vehicle {
    let isConvertible: Bool

    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible
        super.init(isElectric: isElectric)
    }
}


// Copy Classes

// Reference Copy 
class User {
    var username = "Anonymous"
}
var user1 = User()
var user2 = user1
user2.username = "Taylor"
print(user1.username)  
print(user2.username)

// Deep Copy
class User {
    var username = "Anonymous"

    func copy() -> User {
        let user = User()
        user.username = username
        return user
    }
}

// deinitializer 
class User {
    let id: Int

    init(id: Int) {
        self.id = id
        print("User \(id): I'm alive!")
    }

    deinit {
        print("User \(id): I'm dead!")
    }
}

// All users destroyed in scope
for i in 1...3 {
    let user = User(id: i)
    print("User \(user.id): I'm in control!")
}

// Users saved in larger scope
var users = [User]()

for i in 1...3 {
    let user = User(id: i)
    print("User \(user.id): I'm in control!")
    users.append(user)
}

print("Loop is finished!")
users.removeAll()
print("Array is clear!")

// Variables inside classes, we can change them because the signpost is a constant, but the variable data is a variable
// 1. Constant instance, constant property – a signpost that always points to the same user, who always has the same name.
// 2. Constant instance, variable property – a signpost that always points to the same user, but their name can change.
// 3. Variable instance, constant property – a signpost that can point to different users, but their names never change.
// 4, Variable instance, variable property – a signpost that can point to different users, and those users can also change their names.


// Here we change the variable
class User {
    var name = "Paul"
}

let user = User()
user.name = "Taylor"
print(user.name)

// Here we change the signpost
class User {
    var name = "Paul"
}

var user = User()
user.name = "Taylor"
user = User()
print(user.name)
```


