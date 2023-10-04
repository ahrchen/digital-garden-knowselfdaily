---
title: SwiftUI DatePicker
---

### Main Idea
SwiftUI gives us a dedicated picker type called DatePicker that can be bound to a date property. Yes, Swift has a dedicated type for working with dates, and it’s called – unsurprisingly – Date.
    
displayedComponents: can be set to .hourAndMinute and .date 
.labelsHidden() hides the text, but allows for voiceover
in: limits the date options available to the user.

Dates are complicated -> Daylight Savings Time, Leap Year, etc... so use components



```swift
struct ContentView: View {
    
    @State private var wakeUp = Date.now
    
    var body: some View {
        DatePicker("Please pick a date", selection: $wakeUp, displayedComponents: .hourAndMinute)
            .labelsHidden()
        DatePicker("Please enter a date", selection: $wakeUp, in: exampleDates())
            .labelsHidden()
        DatePicker("Please enter a date", selection: $wakeUp, in: self.exampleDates())
            .labelsHidden()
    }
    
    func exampleDates() -> ClosedRange<Date> {
    // create a second Date instance set to one day in seconds from now
    let tomorrow = Date.now.addingTimeInterval(86400)

    // create a range from those two
    let range = Date.now...tomorrow
    return range
}

// Components 
var components = DateComponents()
components.hour = 8
components.minute = 0
let date = Calendar.current.date(from: components) ?? Date.now
}

let components = Calendar.current.dateComponents([.hour, .minute], from: Date.now)
let hour = components.hour ?? 0
let minute = components.minute ?? 0

// Format date and time
Text(Date.now, format: .dateTime.hour().minute())
Text(Date.now, format: .dateTime.day().month().year())
Text(Date.now.formatted(date: .long, time: .shortened))

```


