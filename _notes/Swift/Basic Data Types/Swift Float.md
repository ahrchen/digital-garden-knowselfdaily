---
title: Swift Float
---

### Main Idea

A basic data type that holds a floating point number. Float -> Double(double-precision floating-point number)

```swift


// How to store decimal numbers, the decimal point floats 

// Decimals can cause problems
// 0.1 + 0.3 =   0.30000000000000004 – that 0.3,
// 1 + 2.0 cannot add int and double b./c we want only small error not but one.
// Name = “nick”
// Name = 57 NONONO, cannot change 

// Resolve Decimal rounding issues using ints
// https://www.advancedswift.com/rounding-floats-and-doubles-in-swift/
let floatNum = Double(0.1)
let floatNum2 = Double(0.2)
print(round(((floatNum + floatNum2) * 10)) / 10)

```
