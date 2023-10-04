---
title: SwiftUI Image Interpolation
---

### Main Idea

What happens if you make a SwiftUI Image view that stretches its content to be larger than its original size? By default, we get image interpolation, which is where iOS blends the pixels so smoothly you might not even realize they have been stretched at all. There’s a performance cost to this of course, but most of the time it’s not worth worrying about.

However, there is one place where image interpolation causes a problem, and that’s when you’re dealing with precise pixels. As an example, the files for this project on GitHub contain a little cartoon alien image called example@3x.png – it’s taken from the Kenney Platform Art Deluxe bundle at https://kenney.nl/assets/platformer-art-deluxe and is available under the public domain.

Now you’ll see the alien character retains its pixellated look, which not only is particularly popular in retro games but is also important for line art that would look wrong when blurred.

--https://www.hackingwithswift.com/books/ios-swiftui/controlling-image-interpolation-in-swiftui

```swift
    var body: some View {
        Image("example")
            .interpolation(.none)
            .resizable()
            .scaledToFit()
            .frame(maxHeight: .infinity)
            .background(.black)
            .ignoresSafeArea()
    }


```
