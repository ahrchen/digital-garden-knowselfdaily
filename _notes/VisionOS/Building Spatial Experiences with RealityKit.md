---
title: Building Spatial Experiences with RealityKit
---

###  [Building Spatial Experiences with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10080)

This video goes over the creation of the [Hello World Application](https://developer.apple.com/documentation/visionos/world), focusing on RealityKit in conjunction with SwiftUI. We will learn about how RealityKit works with SwiftUI.

- RealityKit + SwiftUI
    - RealityKit Renders animates, simulates 3D Models and effects and SwiftUI places the RealityKit 3D Engine 
        - Add 3D entities to 2D windows
            - Use Model3D()
        - Create 3D entities in 3D volumes
            - Use WindowGroup() to create Volumetric Window
        - Create 3D entities in Full immersion
            - Use ImmersiveSpace() and RealityView()
    - For more see 
        - [Meet SwiftUI for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10109)
        - [Take SwiftUI to the next dimension](https://developer.apple.com/videos/play/wwdc2023/10113)
        - [Go beyond the window with SwiftUI](https://developer.apple.com/videos/play/wwdc2023/10111)

- Entities and Components
    - Entity is a container object displayed by the 3d Engine Reality Kit
    - Components enable some specific behavior for an entity
    - Example 
        - Earth / Satellite 
            - Model -> material ->  textures + shaders -> How surface mesh responses to light
            - Transform -> Places entity in 3D space position, orientation, scale
                - Note RealityView coordinate system flips the y axis in comparison to SwiftUI so a conversion is needed.
            - Collison and Input Target
                - Needed for interactive objects to gestures
            - Hover effect
                - Needed to highlight object for interaction
                
- RealityView (SwiftUI View Contains RealityKit Entities)
    - async load USD files to add RealityKit entity to Reality View
    - connect obserable state to component properties
    - convert between SwiftUI/RealityKit coordinate space
    - subscribe to events
    - For more see 
        - [Enhance your spatial computing app with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10081)
            
- Input, animation, and Audio
    - Input
        - Gesture Event on Entity with collision and input target component 
            - Add collision and input target components via Reality Composer Pro
                - Create a new USD file and reference the desired USD file 
                - Add the Collision and input target component
                - Update the Collision shape to match 
            - Add Hover Effect to identify the entity as dragable
        - For more see [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083)
    - Animation 
        - From-to-by
        - Orbit
        - Sampling
    - Audio
        - Spatial Audio -> Fixed to subject
        - Ambient Audio -> Fixed to environment
        - Channel Audio -> BG music
        
- Custom Systems
    - Define own component
        - Contains data regarding one aspect of a 3D experience
        - Example 
            - TraceMesh()
    - Define own system
        - Code that act on entities and components
        - Example
            - Supplies the logic and behavior to the TraceMesh()
    - For more see 
        - [Work with Reality Composer Pro content in Xcode](https://developer.apple.com/videos/play/wwdc2023/10273)
        - [Enhance your spatial computing app with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10081)
