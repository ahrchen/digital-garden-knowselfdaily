---
title: Meet RealityKit Trace
---

### [Meet RealityKit Trace](https://developer.apple.com/videos/play/wwdc2023/10099/)

The next step Apple suggest is to learn about the tools, RealityKit Trace. Optimize your rendering performance.

"Discover how you can use RealityKit Trace to improve the performance of your spatial computing apps. Explore performance profiling guidelines for this platform and learn how the RealityKit Trace template can help you optimize rendering for your apps. We'll also provide guidance on profiling various types of content in your app to help pinpoint performance issues." -Apple

#### Rendering
- Shared Space 
    - Your app shares resources with other app on the Rendered server that works with compositor.
- Full Space
    -  Your app has full resources of Rendered server that works with compositor.

#### Profiling spatial apps
- Profile in Isolation
    - Investigate app performance issues
    - Analyze system power impact

- Profile alongside other apps
    - Shared Space

#### Introduction to RealityKit Trace
- Use the real device for accurate times
- Frames 
    - Trace the amount of time to render a frame
    - You should render at 90 fps
- Frame Deadline
    - Early (green)
    - Just in Time (orange)
    - Late (red)
- Average CPU And GPU Frame TIme
- Bottlenecks
- System Power Impact

#### Optimizing offscreen passes
- Zoom into the bottleneck
    - Looking at the metrics 
        - Offscreen loading overloaded
            - Rendered Offscreen not on the display.
            - Shadows (Disable shadows)
            - Masking
            - Rounded rectangles
            - Visual effects
            - For more see [Demystify and eliminate hitches in the render phase](https://developer.apple.com/videos/play/tech-talks/10857)

#### Optimizing asset rendering
- GPU Stalls
    - 3D Render 
        - Frame drops due to too many Triangle and Verticles
        - Check triangles, vertices, and draw cealls
            - Use instancing of same mesh
        - Check statistic with Reality Composer Pro 
            - See [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083)


#### Optimizing system power impact
- System Power Impact too high
    - Profile your application in isolation
- Lower Power impact
    - Render metrics are within expectations
    - Check CPU Workload
        - Time Profiler
            - Find the most expensive cost
    - Check GPU performance states and workload
    - 

#### Overview of optimized World app
- View the app after optimizations

#### Recommendations
- Profile SwiftUI Content
    - SwiftUI Instruments
    - CoreANimation Instruments
    - Hangs Instrument
        - See [Analyze hangs with Instruments](https://developer.apple.com/videos/play/wwdc2023/10248)

- Profile 3D assets
    - Time Profiler for asset loading
    - RealityKit Metric for asset rendering 
    - Check assests using Reality Composer Pro
        - See [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083) 

- Profile Metal Content
    - Use Metal system Trace template 
    - Check GPU timeline and CPU encoding
    - GPU counters and Shader timelines
    - GPU performance state
    - See [Discover Metal debugging, profiling, and asset creation tools](https://developer.apple.com/videos/play/wwdc2021/10157)

