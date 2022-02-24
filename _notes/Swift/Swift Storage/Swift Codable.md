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

// If you want to decode this kind of hierarchical data, the key is to create separate types for each level you have. As long as the data matches the hierarchy you’ve asked for, Codable is capable of decoding everything with no further work from us.

struct User: Codable {
    let name: String
    let address: Address
}

struct Address: Codable {
    let street: String
    let city: String
}

struct ContentView: View {
    
    var body: some View {
        Button("Decode JSON") {
            let input = """
            {
                "name": "Taylor Swift",
                "address": {
                    "street": "555, Taylor Swift Avenue",
                    "city": "Nashville"
                }
            }
            """
            let data = Data(input.utf8)
            let decoder = JSONDecoder()
            if let user = try? decoder.decode(User.self, from: data) {
                print(user.address.street)
            }
        }
    }
}

```
