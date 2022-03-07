---
title: Swift URLSession
---

### Main Idea

SwiftUI’s Image view works great with images in your app bundle, but if you want to load a remote image from the internet you need to use AsyncImage instead. These are created using an image URL rather than a simple asset name, but SwiftUI takes care of all the rest for us – it downloads the image, caches the download, and displays it automatically.



```swift
struct ContentView: View {
    
    var body: some View {
        AsyncImage(url: URL(string: "https://hws.dev/img/bad.png")) { phase in
            if let image = phase.image {
                image
                    .resizable()
                    .scaledToFit()
            } else if phase.error != nil {
                Text("There was an error loading the image")
            } else {
                ProgressView()
            }
        }
        .frame(width: 200, height: 200)
    }
}
```
