---
title: Swift Codable
---

### Main Idea

Swift gives us a fantastic protocol called Codable: a protocol specifically for archiving and unarchiving data, which is a fancy way of saying “converting objects into plain text and back again.”

We’re going to be looking at Codable much more in future projects, but for now we’re going to keep it as simple as possible: we want to archive a custom type so we can put it into UserDefaults, then unarchive it when it comes back out from UserDefaults.

```swift
struct User: Codable {
    let firstUser: String
    let lastUser: String
}
struct ContentView: View {
    @State private var user = User(firstUser: "Taylor", lastUser: "Swift")
        
    var body: some View {
        Button("Save User") {
            let encoder = JSONEncoder()
            
            if let data = try? encoder.encode(user) {
            // That data constant is a new data type called, perhaps confusingly, Data. It’s designed to store any kind of data you can think of, such as strings, images, zip files, and more. Here, though, all we care about is that it’s one of the types of data we can write straight into UserDefaults.
                UserDefaults.standard.set(data, forKey: "UserData")
            }
        }
    }
}

```
