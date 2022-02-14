---
title: Swift App Bundle
---

### Main Idea

When Xcode builds your iOS app, it creates something called a “bundle”. This happens on all of Apple’s platforms, including macOS, and it allows the system to store all the files for a single app in one place – the binary code (the actual compiled Swift stuff we wrote), all the artwork, plus any extra files we need all in one place.

If we want to read the URL for a file in our main app bundle, we use Bundle.main.url(). If the file exists it will be sent back to us, otherwise we’ll get back nil, so this is an optional URL. That means we need to unwrap it like this:

```swift
func loadFile() {
    if let fileURL = Bundle.main.url(forResource: "some-file", withExtension: "txt") {
        // we found the file in our bundle!
        if let fileContents = try? String(contentsOf: fileURL) {
            // we loaded the file into a string!
        }
    }
}
```
