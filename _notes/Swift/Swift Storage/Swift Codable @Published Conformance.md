---
title: Swift Codable @Published Comformance 
---

### Main Idea

Swift already has rules in place that say if an array contains Codable types then the whole array is Codable, and the same for dictionaries and sets. However, SwiftUI doesn’t provide the same functionality for its Published struct – it has no rule saying “if the published object is Codable, then the published struct itself is also Codable.”

As a result, we need to make the type conform ourselves: we need to tell Swift which properties should be loaded and saved, and how to do both of those actions.

First, this initializer is handed an instance of a new type called Decoder. This contains all our data, but it’s down to us to figure out how to read it.

Second, anyone who subclasses our User class must override this initializer with a custom implementation to make sure they add their own values. We mark this using the required keyword: required init. An alternative is to mark this class as final so that subclassing isn’t allowed, in which case we’d write final class User and drop the required keyword entirely.

Third, inside the method we ask our Decoder instance for a container matching all the coding keys we already set in our CodingKey struct by writing decoder.container(keyedBy: CodingKeys.self). This means “this data should have a container where the keys match whatever cases we have in our CodingKeys enum. This is a throwing call, because it’s possible those keys don’t exist.

Finally, we can read values directly from that container by referencing cases in our enum – container.decode(String.self, forKey: .name). This provides really strong safety in two ways: we’re making it clear we expect to read a string, so if name gets changed to an integer the code will stop compiling; and we’re also using a case in our CodingKeys enum rather than a string, so there’s no chance of typos.

There’s one more task we need to complete before the User class conforms to Codable: we’ve made an initializer so that Swift can decode data into this type, but now we need to tell Swift how to encode this type – how to archive it ready to write to JSON.

This step is pretty much the reverse of the initializer we just wrote: we get handed an Encoder instance to write to, ask it to make a container using our CodingKeys enum for keys, then write our values attached to each key.

```swift
class User: ObservableObject, Codable {
    enum CodingKeys: CodingKey {
        case name
    }
    
    @Published var name = "Raymond Chen"
    
    required init(from decoder: Decoder) throws {
        let container = try decoder.container(keyedBy: CodingKeys.self)
        name = try container.decode(String.self, forKey: .name)
    }
    
    func encode(to encoder: Encoder) throws {
        var container = encoder.container(keyedBy: CodingKeys.self)
        try container.encode(name, forKey: .name)
    }
}

struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .padding()
    }
}

```
