---
title: Swift Framework LocalAuthentication
---

### Main Idea
Refer to https://www.hackingwithswift.com/books/ios-swiftui/using-touch-id-and-face-id-with-swiftui
```swift
import LocalAuthentication
import SwiftUI


struct ContentView: View {
    @State private var isUnlocked = false
    
    var body: some View {
        VStack {
            if isUnlocked {
                Text("Unlocked")
            } else {
                Text("Locked")
            }
        }
        .onAppear(perform:  authenticate)
    }
    
    func authenticate() {
        let context = LAContext()
        var error: NSError?
        
        if context.canEvaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, error: &error) {
            let reason = " We need to unlock your data"
            
            context.evaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, localizedReason: reason) { success, authenticationError in
                
                if success {
                    isUnlocked = true
                } else {
                    
                }
                
            }
        } else {
            // no biometerics
        }
    }
}
```


