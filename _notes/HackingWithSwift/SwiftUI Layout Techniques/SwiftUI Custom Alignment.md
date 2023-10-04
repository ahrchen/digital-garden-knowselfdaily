---
title: SwiftUI Custom Alignment
---

### Main Idea

For example, we could update our Twitter code to use .midAccountAndName, then tell the account and name to use their center position for the guide. To be clear, that means “align these two views so their centers are both on the .midAccountAndName guide”.

For more detail https://www.hackingwithswift.com/books/ios-swiftui/how-to-create-a-custom-alignment-guide

```swift

extension VerticalAlignment {
    enum MidAccountAndName: AlignmentID {
        static func defaultValue(in d: ViewDimensions) -> CGFloat {
            d[.top]
        }
    }
    
    static let midAccountAndName = VerticalAlignment(MidAccountAndName.self)
}

struct ContentView: View {
    var body: some View {
        HStack(alignment: .midAccountAndName) {
            VStack {
                Text("@twostraws")
                    .alignmentGuide(.midAccountAndName) { d in d[VerticalAlignment.center] }
                Image(systemName: "person")
                    .resizable()
                    .frame(width: 64, height: 64)
            }
            
            VStack {
                Text("Full name:")
                Text("PAUL HUDSON")
                    .alignmentGuide(.midAccountAndName) { d in d[VerticalAlignment.center] }
                    .font(.largeTitle)
            }
        }
    }
}

```
