---
title: SwiftUI100Days-Project1-WeSplit
---

### Main Idea

This project is a check-sharing app that calculates how to split a check based on the number of people and how much tip you want to leave.

```swift
// Lesson 1: TextFields and keyboards
Form {
    // format: .currency(code: ) will filter out invalid input such as characters. 
    // Locale.current.currencyCode selects for the correct currency for locations
    // $checkAmount is used for two-way(read and write) while checkAmount is for one-way(read)
    Section {
        TextField("Amount", value: $checkAmount, format: .currency(code: Locale.current.currencyCode ?? "USD"))
    }
    
    Section {
        Text(checkAmount, format: .currency(code: Locale.current.currencyCode ?? "USD"))
    }
}

// Lesson 2: Pickers and NavigationView
// We need a NavigationView to present new screens 
NavigationView {
    Form {
        Section {
            TextField("Amount", value: $checkAmount,  format: .currency(code: Locale.current.currencyCode ?? "USD"))
                .keyboardType(.decimalPad)
            // Offers us a picker 
            Picker("Number of people", selection: $numberOfPeople) {
                ForEach(2 ..< 100) {
                    Text("\($0) people")
                }
            }
        }
        
        Section {
            Text(checkAmount, format: .currency(code: Locale.current.currencyCode ?? "USD"))
        }
    }
    // We are placing navigationTitle at the end of the Form insteasd so navigation view is allowed to change titles freely
    .navigationTitle("WeSplit")
}

// Lesson 3: Segmented control for tip percentages
Section {
    Picker("Tip percentage", selection: $tipPercentage) {
        ForEach(tipPercentages, id: \.self) {
            Text($0, format: .percent)
        }
    }
    // Use this modifier to tip picker to make picker segmented
    .pickerStyle(.segmented)
    // Use the following modifier to add header and footer to a section
} header: {
    Text("How much tip do you want to leave?")
}  footer: {
    Text("Is that enough? ")
}

// Lesson 4: Calculated Variable to calculate the total per person 
// Because numberOfPeople, tipPercentage, and checkAmount was marked with the property wrapper @State, the view will update with the new values
// and because totalPerPerson updates with the new values and view is updated, totalPerPerson updates as well. 
var totalPerPerson: Double {
    let peopleCount = Double(numberOfPeople + 2)
    let tipSelection = Double(tipPercentage)

    let tipValue = (checkAmount / 100) * tipSelection
    let grandTotal = checkAmount + tipValue
    let amountPerPerson = grandTotal / peopleCount

    return amountPerPerson
}

// Lesson 5: Hiding the keyboard
struct ContentView: View {
    // Property wrapper specifically designed to handle input focus in our UI
    @FocusState private var amountIsFocused: Bool
    
   var body: some View {
        NavigationView {
            Form {
                Section {
                    TextField("Amount", value: $checkAmount,  format: .currency(code: Locale.current.currencyCode ?? "USD"))
                        .keyboardType(.decimalPad)
                        // HERE -> we use the @FocusState for the .focused modifier this indicates the current focus location 
                        .focused($amountIsFocused)
                }
            }
            .navigationTitle("WeSplit")
            // This allows us to modify the toolbar items for a view
            .toolbar {
                // Lets us place one or more buttons in a specific location specifically here we want a keyboard toolbar
                ToolbarItemGroup(placement: .keyboard) {
                    Spacer()
                    // Button we want to be displayed and sets amountIsFocused to false
                    Button("Done") {
                        amountIsFocused = false
                    }
                }
            }
        }
    }
}
```

