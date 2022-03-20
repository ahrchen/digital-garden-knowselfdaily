---
title: SwiftUI Intergrate UIKit
---

### Main Idea

SwiftUI is a really fantastic framework for building apps, but right now it’s far from complete – there are many things it just can’t do, so you need to learn to talk to UIKit if you want to add more advanced functionality. Sometimes this will be to integrate existing code you wrote for UIKit (for example, if you work for a company with an existing UIKit app), but other times it will be because UIKit and Apple’s other frameworks provide us with useful code we want to show inside a SwiftUI layout.

```swift
// We created a SwiftUI view that conforms to UIViewControllerRepresentable.
// We gave it a makeUIViewController() method that created some sort of UIViewController, which in our example was a PHPickerViewController.
// We added a nested Coordinator class to act as a bridge between the UIKit view controller and our SwiftUI view.
// We gave that coordinator a didFinishPicking method, which will be triggered by iOS when an image was selected.
// Finally, we gave our ImagePicker an @Binding property so that it can send changes back to a parent view.

import PhotosUI
import SwiftUI

struct ImagePicker: UIViewControllerRepresentable {
    @Binding var image: UIImage?
    
    class Coordinator: NSObject, PHPickerViewControllerDelegate {
        var parent: ImagePicker
        
        init(_ parent: ImagePicker) {
            self.parent = parent
        }
        
        func picker(_ picker: PHPickerViewController, didFinishPicking results: [PHPickerResult]) {
            picker.dismiss(animated: true)
            
            guard let provider = results.first?.itemProvider else { return }
            
            if provider.canLoadObject(ofClass: UIImage.self) {
                provider.loadObject(ofClass: UIImage.self) { image, _ in
                    self.parent.image = image as? UIImage
                }
            }
        }
    }
    
    func makeUIViewController(context: Context) -> PHPickerViewController {
        var config = PHPickerConfiguration()
        config.filter = .images
        
        let picker = PHPickerViewController(configuration: config)
        picker.delegate = context.coordinator
        return picker
    }
    
    func updateUIViewController(_ uiViewController: PHPickerViewController, context: Context) {
    }

    func makeCoordinator() -> Coordinator {
        Coordinator(self)
    }
}


import SwiftUI

struct ContentView: View {
    @State private var image: Image?
    @State private var inputImage: UIImage?
    @State private var showingImagePicker = false
    
    var body: some View {
        VStack {
            image?
                .resizable()
                .scaledToFit()
            
            Button("Select Image") {
                showingImagePicker = true
            }
        }
        .sheet(isPresented: $showingImagePicker) {
            ImagePicker(image: $inputImage)
        }
        .onChange(of: inputImage) { _ in loadImage() }
    }
    
    func loadImage() {
        guard let inputImage = inputImage else { return }
        image = Image(uiImage: inputImage)
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}


```
