---
title: Get started with building apps for spatial computing
---

### [Get started with building apps for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10260/)

This video goes over the fundamentals of Spatial Computing, Where to Start, and How to Build

#### Fundamentals

- Shared Spaces (Where App stay side by side)
    - Windows (A single Apps can have multiple windows)
    - Volumes (A volume that displays 3D content more immersively)
- Full Space (Where only your App is Available)
    -  Passthrough (Where you allow the world to come into your full space)
    -  Full Immersion (Allow for hand gestures and Spatial Audio)
- Interact
    - Eyes and Hands Input
        - Taps, long presses, drags
        - Skeletal hand tracking
        - Wireless devices
- Shareplay
    - Sync the same entity, reinforce being in the same place
    - For More See [Design spatial SharePlay experiences](https://developer.apple.com/videos/play/wwdc2023/10075/) and [Build spatial SharePlay experience](https://developer.apple.com/videos/play/wwdc2023/10080)

- Privacy 
    - Privacy-first design
    - Provides curated data and interactions to the app
    - Ask for clear permission

- All the tools you need 
    - Use XCode 
        - Preview (Help view your SwiftUI Code)
        - Simulator (Test your app)
        - Debugger (Visualizations to help identify Collsion shapes, surfaces, etc)
    - Instruments (Actionable insight into your running application and optimize your application)
        - See [Meet RealityKit Trace](https://developer.apple.com/videos/play/wwdc2023/10099)
    - Reality Composer Pro - preview and prepare 3D content for your application
        - To update material for objects [Explore materials in Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10202/)
        - To learn more see [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083)
    - Alternatively Use Unity
        - [Bring your Unity VR app to a fully immersive space](https://developer.apple.com/videos/play/wwdc2023/10093/)
        - [Create immersive Unity apps](https://developer.apple.com/videos/play/wwdc2023/10088/)


#### Where to Start

- Brand new app
    - For more information see [[Develop your first immersive app]]
    - See code samples 
        - [Destination Video](https://developer.apple.com/documentation/visionos/destination-video)
        - [Happy Beam](https://developer.apple.com/documentation/visionos/happybeam)
        - [World](https://developer.apple.com/documentation/visionos/world)
        
- Existing app   
    - iPhone and iPad apps are fully adaptable, select as destination device
        - For more see [Run your iPad and iPhone apps in the Shared Space](https://developer.apple.com/videos/play/wwdc2023/10090/)

#### How to build

- Goes over the project [World](https://developer.apple.com/documentation/visionos/world)
    - Introductions to 3D Model, Volumes, Windows, immersion, shared space
        - Windows
            - Available with SwiftUI
            - 2D and 3D Content
            - Scale and Position 
            - Use with WindowGroup, Model3D
        - Volume
            - Extension of a window
            - Ideal for 3D content
            - Can host multiple views
            - Built for the Shared Space
            - Use with windowStyle(.volumetric) on your WindowGroup
        - RealityView
            - SwiftUI view with Entities
            - RealityKit and SwiftUI deeply integrated
            - Coordinate space conversion
            - SwiftUI Attachments
                - Attach pin onto a globe
            - For more Info: 
                - [Build spatial experiences with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10080) 
                - [Enhance your spatial computing app with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10081/)
        - Spaces
            - Full Space
                - Focus is on your app
                - Place app content anywhere
                - Interact iwth your surroundings
                - Build custom hand interactions [Meet ARKit for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10082/#:~:text=ARKit%20uses%20sophisticated%20computer%20vision,the%20palm%20of%20your%20hand.)
                - Different level of immersion
                    - Passthrough <-> Fully Immersion
                    - .mixed <-> .progressive <-> .full

    
