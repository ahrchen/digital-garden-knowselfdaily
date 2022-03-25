---
title: Swift Documents Directory
---

### Main Idea

letting users create as much data as they want, which means we want a better storage solution than just throwing things into UserDefaults and hoping for the best. Fortunately, iOS makes it very easy to read and write data from device storage, and in fact all apps get a directory for storing any kind of documents we want. Files here are automatically synchronized with iCloud backups, so if the user gets a new device then our data will be restored along with all the other system data – we don’t even need to think about it.

There is a catch – isn’t there always? – and it’s that all iOS apps are sandboxed, which means they run in their own container with a hard to guess directory name. As a result, we can’t – and shouldn’t try to – guess the directory where our app is installed, and instead need to rely on Apple’s API for finding our app’s documents directory.

There is no nice way of doing this, so I nearly always just copy and paste the same helper method into my projects, and we’re going to do exactly the same thing now. This uses a new class called FileManager, which can provide us with the document directory for the current user. In theory this can return several path URLs, but we only ever care about the first one.

### Topics

```swift
struct ContentView: View {
    
    var body: some View {
        Text("Hello World")
            .onTapGesture {
                let str = "Test Message"
                let url = getDocumentsDirectory().appendingPathComponent("message.txt")
                do {
                    try str.write(to: url, atomically: true, encoding: .utf8)
                    let input = try String(contentsOf: url)
                    print(input)
                } catch {
                    print(error.localizedDescription)
                }
            }
    }
    
    func getDocumentsDirectory() -> URL {
        let paths = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)
        return paths[0]
    }
}

```
