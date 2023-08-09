---
title: Develop your first immersive app
---

### [Develop your first immersive app](https://developer.apple.com/videos/play/wwdc2023/10203)

This video goes over creating an immersive view using Xcode, Simulator, and Reality Composer Pro. It is a great way to get familiar with the development environment. 

#### Create an Xcode Project

- Types of initial VisionOS Projects
    - Initial Scene
        - Windows - A 2D window in 3D space - For more see [Meet SwiftUI for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10109/)
        - Volumes - A 3D volume to display 3D objects - For more see [Take SwiftUI to the next Dimension](https://developer.apple.com/videos/play/wwdc2023/10113)
    - Immersive Space - Unbounded content on infinite canvas -> For more see [Go beyond the window with SwiftUI](https://developer.apple.com/videos/play/wwdc2023/10111)
        - Mixed Immersion - 3D objects in the real world
        - Progressive Immersion - 3D objects in a 180 degree virtual world adjustable by user
        - Full Immersion - 3D in 360 degree virtual world

- Select an Initial Scene with Volumes and No Immersive Space
    - First file is MyFirstImmersiveApp has a WindowGroup
        - WindowGroup specifies the top level SwiftUI views that your app presents
    - Second file is ContentView hold most of the code displayed by WindowGroup
        - Two Views RealityView and ToggleView
            - RealityView generates content in the first parameter and updates content on SwiftUI state change in the second parameter. Gesture added to RealityView to allow tap on entity to toggle - For more see [Build spatial experiences with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10203#:~:text=Build%20spatial%20experiences%20with%20RealityKit)

#### Simulator

- How to use the simulator.
    - Viewing Controls
    - The toolbar for different scenes
    - For more info: https://developer.apple.com/documentation/visionos/interacting-with-your-app-in-the-visionos-simulator

#### Xcode Previews

- Use to quickly preview the SwiftUI View Changes

#### Reality Composer Pro

- Prepare, preview, edit 3D content, organize content into scenes
- How to use Reality Composer Pro
    1. Create a new scene
    2. Coordinate System uses your feet as the origin x -> right, y -> up, and -z -> forward
    3. To get hand data use ARKit - [Meet ARKit for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10082)
    4. Follow the tutorial 
    5. For more see
        - [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083)
        - [Work with Reality Composer Pro content in XCode](https://developer.apple.com/videos/play/wwdc2023/10273)
    

#### Create an Immersive scene

- Add Immersive Space to MyFirstImmersiveApp below the WindowGroup and display ImmersiveView()
- Create ImmersiveView() to be displayed 
- Create button to open ImmersiveView() in ContentView()

#### Target gestures to entities
- use ".gesture(TapGesture().targetedToAnyEntity().onEnded { value in" on entity with CollisionComponent and InputTargetComponent
- Add the CollisionComponent and InputTargetComponent using the RealityComposerPro
- Add code to the RealityView to move clouds

