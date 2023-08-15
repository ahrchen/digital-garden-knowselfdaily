---
title: Take SwiftUI to the next dimension
---

### [Take SwiftUI to the next dimension](https://developer.apple.com/videos/play/wwdc2023/10113)

This video provides several key tips on creating SwiftUI Volumes for visionOS. 

#### Volumes

- Can use without any windows
- Provides a fixed scale container
- Unlike windows, maintains the same size at any distance
- Horizontally aligned, and support viewing from any angle
- Doesn't take over the entire space
- Use .windowStyle(.volumetric) modifier on a WindowGroup

#### 3D views and layout

- Model3D
   - A RealityKit view to load simple 3D scenes asynchronously
        - Similar to AsyncImage, you can use placeholders during loading
        - Use .resizable modifier with model, similar to Image
        - Default alignment is against back plane. Otherwise, use .frame(depth:alignment:) with .front alignment
        - Can use .glassBackgroundEffect() to make text labels readable in visionOS
        - Can use TimelineView(.animation) to animate the content to spin according to time wieh  .rotation3DEffect()

#### RealityView

- Use for more involved 3D scenes

- Can use RealityKit's Entity-Component system for advanced rendering

- RealityView attachments
    - Pair tagged (.tag) SwiftUI views with Entity inside RealityView
    - Useful for adding annotations or editing affordances
    - These live views can respond to state changes, run animations, and handle gestures
- For More See 
    - [Build spatial experiences with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10080) 
    - [Enhance your spatial computing app with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10081)

#### 3D gestures

- Existing gestures supported in 3D
    - Hands, eyes, trackpad mechanics supported

- Tap to Add Favorite location on Earth Entity
    - Add InputTargetComponent to RealityKit Entity to receive input

    - CollisionComponent is used to define shape of entity's interactive region

    - Can use SpatialTapGesture to allow user to interact with entity

        - .targetedToEntity modifier ties gestures to specific entities

        - Convert from SwiftUI local space to scene's coordinate space

- Instead of loading another model using RealityKit, you can add a Model3D as an attachment

- More Gestures
    - RotateGesture3D 
    - manipulationGesture 
    - magnifyGesture
