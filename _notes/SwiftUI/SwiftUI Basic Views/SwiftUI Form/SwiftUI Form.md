---
title: SwiftUI Form
---

### Main Idea
Forms are scrolling lists of static controls like text and images, but can also include user interactive controls like text fields, toggle switches, buttons, and more. The maximum number of items in a form is 10. Beyond 10, you need use a group. To make the form split up the items use section

#### Topics
- [[SwiftUI Stepper]]
- [[SwiftUI DatePicker]]
- [[SwiftUI Form Validation]]
- [[SwiftUI TextEditor]]

```swift
var body: some View {
    Form {
        Text("Hello, world!")
            .padding()
        Group {
            Text("Hello, world!")
            Text("Hello, world!")
        }
        Section {
            Text("Hello, world!")
            Text("Hello, world!")
        }
    
    }
}

```


