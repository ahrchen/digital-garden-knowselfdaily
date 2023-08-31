---
title: Go beyond the window with SwiftUI
---

### [Go beyond the window with SwiftUI](https://developer.apple.com/videos/play/wwdc2023/10111/)

This video provides several key tips on creating SwiftUI ImmersiveSpace for visionOS. 

#### Get Started with Space

- Scene type ImmersiveSpace
    - Only on full space at a time, the previous one must be dismissed before a new full space can be introduced
    - Has it's only coordinate system, using the user as the origin

#### Display content

- Use RealityView - See [Build spatial experiences with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10080) for more
    - Asynchronous loading
    - ARKit anchor-based placement
    - Use of hands and head-pose data

#### Managing your Space

- Scene Phases
    - Active and Inactive phases
    
- Coordinate Conversions
    - GeometryReader3D
        - transform to center of immersiveSpace

    - SharePlay - [Build spatial SharePlay experiences](https://developer.apple.com/videos/play/wwdc2023/10087)
        - Private Immersive Space
        - Group Immersive Space

- Immersion Styles
    - Select style based on size of magnification
        - Mixed
        - Progressive
        - Full

#### Customization

- Immersive Space at Launch 
- Hand Tracking + Virtual Hands
    - Space Gloves - [Evolve your ARKit app for spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10091/)
