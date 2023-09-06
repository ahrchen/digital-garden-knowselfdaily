---
title: Meet SwiftUI for spatial computing
---

### [Meet SwiftUI for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10109/)

This video provides a quick overview the SwiftUI Scenes that make up the building blocks of your app, Windows, Volumes, and Full Spaces. You will learn about the new features that are now available, but for a full tutorial, you will need to dive deeper.

#### Windows - See Tutorial Here [[Elevate your windowed app for spatial computing]]

- Ornament 
    - Place accessories outside the window's bounds. Used in TabView,  presentations, and more. Make your own using the .ornament modifier.
        - Display additional control outside the window.
    
- StatsGrid to form cards for stats
    - Button to interface into the card

- Interaction
    - Eyes: Look at an element and use an indirect pinch gesture.
    - Hands: reaching out and touching apps.
    - Pointer: trackpad, hand gesture or hardware keyboard.
    - Accessibility: e.g. VoiceOver, Switch Control.- See [Create accessible spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10034)
    - Gestures have been updated
    
- Hover effects
    - Critical to making your app responsive.
    - Run outside of your app's process.
    - Added automatically to most controls.
    - If you're using a custom control style, make sure to add hover effects to make them responsive and easy to use.
    - As simple as adding a .hovereffect modifier

#### Volumes - See More [[Take SwiftUI to the next dimension]]

- To add a volume, specify .windowStyle(.volumetric) on your WindowGroup.

- Model3D
    - To display a 3D model, use the new Model3D API from RealityKit.
    - A Model3D always loads asynchornously. Similar to AsyncImageView, a Model3D can display a placeholder view.
    - Layouts like ZStack are automatically aware of the depth of your content.

- RealityView - See Tutorial Here [Build spatial experiences with RealityKit](https://developer.apple.com/videos/play/wwdc2023/10080)
    - RealityView provides easy access to the full power of RealityKit Pro.
    - SpatialTapGesture gives the full 3D location of the tap.
    - the tagetedToAnyEntity view modifier provides context like the entity you tapped on and the location relative to that entity.
    - RealityView attachments allow mixing custom SwiftUI views together, inline with RealityKit entities.


#### Full Spaces - See Tutorial Here [[Go beyond the window with SwiftUI]]

- ImmersiveSpace
    - Add an ImmersiveSpace scene.
    - Provide an id to the space so you can programmatically open it from your main window.
    - To open the space, use the new openImmersiveSpace environment action.
    
- Immersion styles
    - Mixed, Progressive and Full immersion are supported.
    - With Progressive immersion, you can use the digital dial to dial in how much immersion feels right to you.
    - Use the immersionStyle view modifier.

- ARKit - See More Here [Meet ARKit for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10082)
    - Gain rich understanding of the real world
    - Place content near phyiscal surfaces
    - Build powerfull hand gestures
     
