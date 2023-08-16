---
title: Evolve your ARKit app for spatial experiences
---

### [Evolve your ARKit app for spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10091/)

This video provides several key tips on bringing your iPadOs and iOS ARKit expeerience to Spatial Computing.

#### Overview 0:00

- Introduced ARKit in 2017
- Tracks your device with 6 degrees of freedom
    - Allows for anchoring
- Scene Understanding
    - Geometry and semantic knowledge for placement
- Rendering 
    - SceneKit -> RealityKit
- ARKit and RealityKit deeply integrated
- Built in camera passthrough and hand matting
- World map persistence is a system service

#### Prepare your experience

- Present your app
    - Shared Space
    - Full Space
        - AnchorEntity
        - ARKit

- Prepare your content
    - USD -> Reality Composer Pro -> Xcode
        - Edit materials & RealityKit components
    - See [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083)


#### Use RealityView

- Mix and match 2D and 3D 
- Container for entities
    - Entity component system 
    - ![](https://hackmd.io/_uploads/Sk0K6p53h.png)

- Interact with SwiftUI Gestures
- Realistic simulations with surroundings

- Very Similar to ARView
        - ARView similar to RealityView
        - Scene similar to Content
        - AnchorEntity must ARSession in iOS while RealityView does not need permissions
    - ![](https://hackmd.io/_uploads/S1BVCp533.png)

#### Bring in your content

- Shared Space
    - Add entities to your view
    - Relative to space origin
    - Can interact with other entities in the space
- Full Space
    - AnchorEntity 
        - No user permission required
        - Transforms not shared
        - support hands
        - ARKit - placement logic
            - Use ARKit Scene understanding
            - Leverage ARKit anchor data
            - Utilize world anchor
            - Transforms are relative to space origin
            - Requires user permission 

#### Raycasting

- Ray casting provides a 3D location in physical space that corresponds to a given 2D location on the screen. When you call this function, it succeeds in returning a result when a mathematical ray that ARKit casts outward from the user intersects with any real-world surfaces that ARKit detects in the physical environment. 
    - Requires collision components
        - MeshAnchor for each item in the world
        - ![](https://hackmd.io/_uploads/BJcUZ0523.png)

    - Raycast with System Gestures or Hand Tracking
        - SpatialTapGesture
            - ![](https://hackmd.io/_uploads/Bym0-R9hh.png)
        - Hand Anchors
            - ![](https://hackmd.io/_uploads/SJDeGC932.png)

    - Add world anchor
        - ![](https://hackmd.io/_uploads/ryqWfRc3n.png)

    - Combine the elements
        - ![](https://hackmd.io/_uploads/S1s7MAq2n.png)

    - Interact with it
        - ![](https://hackmd.io/_uploads/rk8JQR933.png)

#### ARKit updates

- Run your session 
    - iOS have mutiple tracking configurations
        - AROrientationTrackingConfiguration
        - ARImageTrackingConfiguration
        - ARWorldTrackingConfiguration
        - ARPositional TrackingConfiguration
    - Spatial computing
        - HandTrackingProvider
        - SceneReconstructionProvider
        - ImageTrackingProvider
        - PlaneDetectionProvider
        - WorldTrackingProvider

    - So you have your own selection of anchors you would like to recieve.


- recieve anchor updates 
    - iOS 
        - ARSessionDelegate
            - ARFrame 
                - Anchors
    - Spatial Computing
        - Providers decoupled from the Frame
            - Anchor updates
    

- persist world anchors
    - iOS: multiple steps
        - Application
            - Save map
            - Load map
            - Relocalize
            - Get anchors
            - Show content
    - Spatial computing: Handles the map
        - System
            - Save map
            - Load map
            - Relocalize
        - Application
            - WorldTrackingProviders
            - Get Anchors
            - Show Content
