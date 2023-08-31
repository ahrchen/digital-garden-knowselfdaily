---
title: Optimize app power and performance for spatial computing
---

### [Optimize app power and performance for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10100/)

The next step Apple suggest is to learn about the tools, learn to use optimize your application.

"Learn how you can create powerful apps and games for visionOS by optimizing for performance and efficiency. We'll cover the unique power characteristics of the platform, explore building a performance plan, and share some of the tools and strategies to test and optimize your apps." -Apple

#### Explore performance with spatial computing
- Continuously updating content
    - Renders every frame at all times
    - Computes spatial algorithms continuously
    - Run multiple apps at the same time
        - Responsiveness
        - Immersion
        - Comfort

- Measure performance metrics - For more details see  [Ultimate application performance survival guide](https://developer.apple.com/videos/play/wwdc2021/10181)
    - Power
        - Thermal Pressure
    - Hangs
        - Main Thread is stalled 
    - Rendering
        - Essential for static content as well as active 
    - Launch Time
    - Disk Writes
    - Memory
    - Terminations
    

#### Profile your app
- Development and testing
    - XCTest Performance tests
    - Xcode Gauges
    - Instruments
        - [Meet RealityKit Trace](https://developer.apple.com/videos/play/wwdc2023/10099)
    - Profile many scenarios
        - Profile on device
        - Use different user input methods
        - Play audio and video
        - Use FaceTime
        - Check sustained performance
        - Run multiple apps

- Beta and Public release
    - MetricKit
        - Energy dionostics
- Public Release
    - Xcode Organizer



### Optimize your app

#### Explore render performance
- Render pipeline
<img src="/assets/RenderPipeline.png"/>

- App needs the to recieve frame from rendering deadline, otherwise lag

#### Optimize SwiftUI and UIKit content for render performance
- Rendering static UI costs
    - System renders static UI content
    - Translucency and overlap generate overdraw
- Optimize static UI rendering
    - Minimize translucency and overlap with Z offset
    - Lower the default window sizes
- Redrawing UI costs
    - Dynamic content scaling with user eye input
        - More frequent redrawing at different scales
        - SwiftUI and UIKit enable this by default
        - For more see [Explore rendering for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10095)
- Optimize UI redraws
    - Reduce offscreen render passes
        - Shadow, Blur, Masking reduced
    - Eliminate unnecessary UI view updates
        - Use @Observable with SwiftUI View
            - Provides more granular UI change tracking and reduce unneeded Updates

#### Optimize RealityKit content for render performance
- Optimize 3D scene
    - 3D scene types
        - Mesh rendering
        - Animations
        - Audio
        - Attachments
        - Particles
        - Physics
        - Video
        - Portals
    - Reality Composer Pro helps combine assets to create scenes
        - Simple assets have lower statistics
        - For more see [Create 3D models for Quick Look spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10274)


- Optimize mesh rendering
    - Reduce mesh parts, triangles, and vertex counts
    - Minimize overdraw from transparency
    - Using "Physically Based" versus "Custom" material in Reality Composer Pro
    - For more see [Explore materials in Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10202) and [Explore rendering for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10095)

- Optimize Render updates
    - Your app sends updates to render server
        - Common causes of expensive updates
            - Frequent entity creation and destruction
            - Complex animation
            - Frequent SwiftUI redraws
            - Loading too many assets
    - Optimize entity render updates
        - Create entities in advance and show them as needed
        - Flatten entity hierarchies
        - Minimize updates from code-based animations
        - Avoid excessive SwiftUI redraws from RealityKit entity updates
- Optimize RealityKit asset loading
    - Use asynchronous-loading APIs
    - Load assets in advance
    - Reuse assets between entities
    - Export with Reality Composer Pro
    - Reduce asset size
- Optimize fully immersive content
    - Reduce GPU work per pixel
    - Optimize for GPU power use
    - Use unlit "custom" materials in Reality Composer Pro

#### Optimize Metal apps for render performance
- Send your Metal app straight to the Compositor
    - See [Discover Metal for immersive apps](https://developer.apple.com/videos/play/wwdc2023/10089/)

- Optimize for CompositorServices
    - Pace rendering for compositor render rate
    - Query new input data each frame
    - Query input data right before GPU encoding
    - Meet render deadlines
- Optimize GPU usage
    - Profile with Metal System Trace template
    - Heavy fragment and vertex work impacts system rendering
    - Reduce ALU instructions and texture accesses by shaders
    - Use Metal compute shaders
- For more see
    - [Optimize Metal apps and games with GPU counters](https://developer.apple.com/videos/play/wwdc2020/10603)
    - [Delivering Optimized Metal Apps and Games](https://developer.apple.com/videos/play/wwdc2019/606)
    - [Metal Game Performance Optimization](https://developer.apple.com/videos/play/wwdc2018/612)

#### Learn about user input performance

- Input Response Times
    - Eyes, Hands, Voice, Hardward
        - These are processed on the main thread
    - Input response time depends on display refresh rate
    - At 90 Hz, aim to keep updates below 8ms
- Optimize interactive content
    - Use static colliders over dynamic colliders for RealityKit content
    - Minimize overlapping interactive content to reduce hit testing

#### Optimize ARKit usage

- Always-on ARKit algorithms to anchor items
- Optimize for anchoring work
    - Anchors contribute to computational needs
    - Consider if anchors need to be tracked continuously
        - Use TrackingMode.once on AnchorComponents
        - Minimize persised and transient anchor counts
- Optimize ARKit data use
    - Query latest ARKit Data
    - Pose Prediction queries are not free
    - Toggle collision data generation for scene understanding meshes


#### Explore audio and video playback performance
- Spatial Audio
    - Spatial Audio is used by default
    - Requires real-time computation work
- Optimize Spatial Audio
    - Concurrent playback
    - Moving sources
    - Sound stage size
- Video playback
    - Each video frame needs to be decoded and rendered 
- Optimize video
    - Minimize UI and 3D render updates
    - Use different video frame rates
    - Reduce concurrent playback
- Video presentation methods
    - See [Create a great spatial playback experience](https://developer.apple.com/videos/play/wwdc2023/10070)


#### Bring great performance to SharePlay experiences
- Sustain great performance over time
- Optimize for long-running experiences
    - Start with great sustained performance offline
    - Profile rendering and input on both sides
    - Profile for power consumption
    - Turn off unneeded features during SharePlay


#### Avoid terminations from thermal and memory pressure

- Adapt to thermal pressure
    - Critical thermal pressure
        - Slows down app
        - Shuts down app
    - Do less work
    - ProcessInfo.thermalStateDidChangeNotification
    - Use thermal inducers 
- For more see [Designing for Adverse Network and Temperature Conditions](https://developer.apple.com/videos/play/wwdc2019/422)

- Memory pressure
    - Critical memory pressure
        - Shut down least recently used app
        - Shut down overused memory app
    - Reduce Memory usage
        - Reduce UI rendering memory allocations
        - Reduce RealityKit's texture and geometry memory
        - Evaluate total audio and video memory use
    - For more see 
        - [Profile and optimize your game's memory](https://developer.apple.com/videos/play/wwdc2022/10106)
        - [Detect and diagnose memory issues](https://developer.apple.com/videos/play/wwdc2021/10180)
        - [iOS Memory Deep Dive](https://developer.apple.com/videos/play/wwdc2018/416)
