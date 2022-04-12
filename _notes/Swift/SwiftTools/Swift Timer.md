---
title: Swift Timer
---

### Main Idea

We use the timer class to trigger events repeatedly.
every: 1 <- Every one second
tolerance: 0.5 <- Give or take 0.5 seconds to save battery life
on: .main <- On the main thread 
in: .common <- On the common run loop (Handles running code while the user is actively doing something, such as scrolling in a list)
.onReceive(timer) <- the timer is a publishedd that announces changes, we need to catch the announcement by hand using .onReceive 
self.timer.upstream.connect().cancel() <- Cancel the timer
For more information see https://www.hackingwithswift.com/books/ios-swiftui/triggering-events-repeatedly-using-a-timer 
```swift
struct ContentView: View {
    let timer = Timer.publish(every: 1, tolerance: 0.5, on: .main, in: .common).autoconnect()
    @State private var counter = 0
    
    var body: some View {
        Text("Hello World")
            .onReceive(timer) { time in
                if self.counter == 5 {
                    self.timer.upstream.connect().cancel()
                } else {
                    print("The time is now \(time)")
                }
                self.counter += 1
            }
    }
}

```
