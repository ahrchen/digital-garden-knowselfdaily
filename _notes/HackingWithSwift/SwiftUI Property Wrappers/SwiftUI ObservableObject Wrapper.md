---
title: SwiftUI ObservableObject Wrapper
---

### Main Idea

Classes that conform to the ObservableObject protocol can use SwiftUI’s @Published property wrapper to automatically announce changes to properties, so that any views using the object get their body property reinvoked and stay in sync with their data. That works really well a lot of the time, but sometimes you want a little more control and SwiftUI’s solution is called objectWillChange.

Every class that conforms to ObservableObject automatically gains a property called objectWillChange. This is a publisher, which means it does the same job as the @Published property wrapper: it notifies any views that are observing that object that something important has changed. As its name implies, this publisher should be triggered immediately before we make our change, which allows SwiftUI to examine the state of our UI and prepare for animation changes.

We can use @Published to automatically update the UI, we CAN also change notifications manually using the objectWillChange property I mentioned earlier. This lets us send the change notification whenever we want, rather than relying on @Published to do it automatically.


### Usage

```swift
import SwiftUI

@MainActor class DelayedUpdater: ObservableObject {
    var value = 0 {
        willSet {
            objectWillChange.send()
        }
    }
    
    init() {
        for i in 1...10 {
            DispatchQueue.main.asyncAfter(deadline: .now() + Double(i)) {
                self.value += 1
            }
        }
    }
}

struct ContentView: View {
    @ObservedObject var updater : DelayedUpdater
    
    init() {
        _updater = ObservedObject(wrappedValue: DelayedUpdater())
    }
    
    var body: some View {
        Text("Value is: \(updater.value)")
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

```
