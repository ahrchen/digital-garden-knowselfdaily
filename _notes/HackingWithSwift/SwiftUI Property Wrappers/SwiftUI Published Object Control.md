---
title: Swift ObservableObject Manually Publishing Changes
---

### Main Idea

We use willSet to add additional functionality to @published value in ObservableObject class

```swift

class DelayedUpdater: ObservableObject {
//    @published var value = 0
//    Below we use willSet so that we can add additional functionality to published event
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
    @ObservedObject var updater = DelayedUpdater()
    
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
