---
title: Enhance your spatial computing app with RealityKit
---

### [Enhance your spatial computing app with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10081/)

This video provides several key tips on creating SwiftUI RealityKit for visionOS. 

#### RealityView attachments

- How to embed SwiftUI views into RealityKit content using attachments in RealityView 02:05
    - Attachments are a useful way to embed SwiftUI content into your RealityKit scene.
    - Example app that demonstrates how to put text labels and views alongside 3D content using attachment views.
        - 2 parts to settings up attachments 
            - 1. Add the parameter in the make closure of your RealityView 
            - 2. Include the attachments view builder to your RealityView
        - The attachments view builder is where you can provide SwiftUI views that you want to add to your RealityKit content. You can then tag those views and call them as entities inside your make closure using the call entity(for:). 


- How to use multiple attachments inside of a make closure 04:32

- You can also update entities inside of the update closure whenever there are changes to SwiftUI view state.
- For more see [Work with Reality Composer Pro content in Xcode](https://developer.apple.com/videos/play/wwdc2023/10273)



#### Video playback 06:17

- VideoPlayerComponent is a new component type in RealityKit used for embedding video content inside a 3D scene. - Reminder: components define behavior that you attach to entities.
    - To play a video using VideoPlayerComponent: 
        - 1. Load a video file from resources bundle 
        - 2. Create an AVPlayer instance 
        - 3. Create a VideoPlayerComponent 
        - 4. Attach component to an entity
![](https://hackmd.io/_uploads/S1666PFh3.png)
    - Since RealityKit is a 3D framework, video is represented as an entity with a mesh so that you can move and position it in 3D space.
    - VideoPlayerComponent also supports Passthrough Tinting by setting the isPassthroughTintingEnabled property to true.
    - You can also subscribe to VideoPlayerEvents by calling the subscribe function inside RealityViews content, and specifying the event type and entity 10:39.
        - ContentTypeDidChange
        - ViewingModeDidChange
        - VideoSizeDidChange
        
- Learn more about video content including 3D videos in [Deliver video content for spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10071)


#### Portals

- Portals create openings to other worlds that are visible through mesh surfaces. Entities inside of these worlds use separate lighting, and are masked by portal geometry.

    - To make a portal, you must first create a World. You doing this by adding a World component to an entity. Add content to the world by attaching entities as children of the world entity. Note: entities in a world are only visible through a portal surface

    - Once you have your World entity, you create a mesh with a portal material, then add a portal component targeted to the world entity. See 13:15

![](https://hackmd.io/_uploads/HyAbguF33.png)

- Basically there's a separate component called World which is what you use in portals 
- Lighting is unique and can learn more in [Explore rendering for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10095)
- Schematics for how Portals are built 15:00


#### Particle emitters 15:04

- ParticleEmitterComponent provided in RealityKit can be created either Reality Composer Pro or via RealityKit at runtime.

    - The ParticleEmitterComponent contains many properties that control various aspects of particle look and behavior.
    - Code walkthrough of building a particle system 15:49.
- For more see [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083)

#### Anchors

- Anchors in RealityKit can be used to place content on surfaces, such as walls, floors, or locations relative to head and hands.

- Anchors support 2 tracking modes: 
    - 1. .continuous - anchor entity moves along with the anchor over time, such as when your head moves. 
    - 2. .once - anchor entity will not move after being positioned once.

- You can listen to when an entity becomes anchored by subscribing to the AnchoredStateChanged event in RealityKit.

- Anchor transforms are not accessible to the app. In order to get access to anchor transforms, you will need to use ARKit. [Meet ARKit for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10082)

- Code walkthrough of setting an anchor in your app 18:18.


