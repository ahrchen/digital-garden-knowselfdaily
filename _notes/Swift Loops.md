---
title: Swift Loops
---

### Main Idea
Loops allow us to repeat a simple task billions of times every second. YOu can read sensor data, redraw screen 120 times a second. 


```swift
// Loop over an array

let platforms = ["iOS", "macOS", "tvOS", "watchOS"]

// Loop iteration, cycling the loop variable os.
for os in platforms {
    // Loop Body
    print("Swift works great on \(os).")
}

// Loop of a range of numbers 
for i in 1...12 {
    print("5 x \(i) is \(5 * i)")
}

// Nested Loop
for i in 1...12 {
    print("The \(i) times table:")

    for j in 1...12 {
        print("  \(j) x \(i) is \(j * i)")
    }

    print()
}

// ..< to count from 0 up to but excluding number of items in the array
for i in 1..<5 {
    print("Counting 1 up to 5: \(i)")
}

// Use _ when you don't need the variable 
let names = ["Sterling", "Cyril", "Lana", "Ray", "Pam"]

for _ in names {
    print("[CENSORED] is a secret agent!")
}

// Print 1 until end of array
print(names[1...])

// Print from beginning of array til end
print(names[...2])

// While Loop, used when we do not know when the loop will end
var countdown = 10

while countdown > 0 {
    print("\(countdown)…")
    countdown -= 1
}

print("Blast off!")

let id = Int.random(in: 1...1000)
let amount = Double.random(in: 0...1)

// create an integer to store our roll
var roll = 0

// carry on looping until we reach 20
while roll != 20 {
    // roll a new dice and print what it was
    roll = Int.random(in: 1...20)
    print("I rolled a \(roll)")
}

// if we're here it means the loop ended – we got a 20!    
print("Critical hit!")

// BREAK And CONTINUE

// continue is used generally at the beginning of a loop to ignore certain items.
let filenames = ["me.jpg", "work.txt", "sophie.jpg", "logo.psd"]

for filename in filenames {
    if filename.hasSuffix(".jpg") == false {
        continue
    }

    print("Found picture: \(filename)")
}

// break is used to exit the loop if a certain condition is hit...aka done my job
let number1 = 4
let number2 = 14
var multiples = [Int]()

for i in 1...100_000 {
    if i.isMultiple(of: number1) && i.isMultiple(of: number2) {
        multiples.append(i)

        if multiples.count == 10 {
            break
        }
    }
}

print(multiples)

```


