---
title: SwiftUI Scenes
---

### Main Idea

How to be notified when your SwiftUI app moves to the background
SwiftUI can detect when your app moves to the background (i.e., when the user returns to the home screen), and when it comes back to the foreground, and if you put those two together it allows us to make sure our app pauses and resumes work depending on whether the user can see it right now or not.

-  Active scenes are running right now, which on iOS means they are visible to the user. On macOS an app’s window might be wholly hidden by another app’s window, but that’s okay – it’s still considered to be active.
- Inactive scenes are running and might be visible to the user, but they user isn’t able to access them. For example, if you’re swiping down to partially reveal the control center then the app underneath is considered inactive.
- Background scenes are not visible to the user, which on iOS means they might be terminated at some point in the future.

For more information see - https://www.hackingwithswift.com/books/ios-swiftui/how-to-be-notified-when-your-swiftui-app-moves-to-the-background

### Usage

```swift
struct ContentView: View {
    @Environment(\.scenePhase) var scenePhase
    
    var body: some View {
        Text("Hello word")
            .padding()
            .onChange(of: scenePhase) { newPhase in
                if newPhase == .active {
                    print("Active")
                } else if newPhase == .inactive {
                    print("Inactive")
                } else if newPhase == .background {
                    print("Background")
                }
            }
    }
}
```
