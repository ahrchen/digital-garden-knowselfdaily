---
title: Create immersive Unity apps
---

### [Create immersive Unity apps](https://developer.apple.com/videos/play/wwdc2023/10088/)

The next step Apple suggest is to learn about the Unity, lets check out when and where we should Unity.

"Explore how you can use Unity to create engaging and immersive experiences for visionOS. We'll share how Unity integrates seamlessly with Apple frameworks, take you through the tools you can use to build natively for the platform, and show you how volume cameras can bring your existing scenes into visionOS windows, volumes, and spaces. Discover how to incorporate visionOS features like passthrough and scene understanding, customize your visuals with Shader Graph, and adapt your interactions to work with spatial input."
-Apple

####  Achieve your visual look
- We can create immersive and fully immersive scenes
- For Fully Immersive Scenes see [Bring your Unity VR app to a fully immersive space](https://developer.apple.com/videos/play/wwdc2023/10093)

- To display Unity Assets from Asset Store in Shared Space convert them for use in RealityKit 
    - Use Unity PolySpatial to Translate Unity Assets
        - Materials
            - Physically Based materials
                - Via Universal render pipeline 
                    - Lit
                    - Simple Lit
                    - Complex Lit
                - Via Built-in render pipeline
                    - Standard
            - Custom 
                - Unity Shader Graph -> MaterialX -> ShaderGraphMaterial
                - Handwritten Textures are not supported thru RealityKit
                    - RenderTexture via Unity -> TextureGraph -> RealityKit
            - Special Effect Materials
                - Unlit
                    - Create objects with solid color without effect of environment
                - Occulusion
                    - Passthrough show through object
                    - You can use the Occlusion Shader with world mesh data to help your content feel more integrated with the real world.


        - Mesh Renderers
            - Unity MeshRenderers and SkinnedMeshRenderers are supported and are the primary way of bringing visual content into real space.
            - Rigged characters and animation are available.
            - You can use either the Universal or the Built-in Render Pipeline, and your content will be translated to RealityKit via Unity PolySpatial.
            - Rendering features, such as postprocessing effects and custom pipeline stages, are not available, as RealityKit performs the final rendering.




        - Particle Effects
            - Particle effects using Unity's Shuriken system are either translated to RealityKit's particle system, if they are compatible, or are translated to baked meshes.


        - Spites
            - Sprites become 3D meshes, though you should consider how you're using them in a spatial context.
        - Simulation features
            - PolySpatial works to optimize and translate rendering between Unity and RealityKit.

            - Simulation features in Unity work just like you're used to, such as Physics, Animation and Timeline, Pathfinding and NavMesh, your custom MonoBehaviours, and other non-rendering features.


####  Play to device
- Helps save time
    - To help you fine-tune your look and to speed up iteration, Unity PolySpatial enables "Play to device." It can take time to go through the build process to see what your content looks like on your device.
        - With PolySpatial, you have access to Play to device for the first time.

            - Play to device lets you see an instant preview of your scene and make live changes to it.

        - It works in the simulator and works great on device as well.

        - You can use Play to device to rapidly explore the placement and size of your content, including adding and removing elements.

        - You can change materials, textures, and even Shader Graphs to fine-tune your look while seeing your content in place with passthrough.

        - You can test out interaction because events are sent back to the editor.

        - Your simulation continues to run, so it's easy to debug just by attaching to the editor.

- Example Here's the same castle scene you saw earlier.

    - I have it open in Unity on the left, and with Play to device, I can see it running in the simulator on the right.

        - I can add more ogres just by dragging them into my scene.

        - They're instantly visible in the simulator or device.

        - If I want to see how pink or neon green ogres look, I can.

- Play to device is a really efficient workflow for iterating on your content, and it's currently available in Unity only for creating content in the shared space.

#### Explore volume cameras
##### Because you're using Unity to create volumetric content that participates in the shared space, a new concept called a volume camera lets you control how your scene is brought into the real world.

- A volume camera can create two types of volumes, bounded and unbounded, each with different characteristics.

    - Your application can switch between the two at any time.

    - Bounded volumes exist in the shared space as volumes, alongside other apps and games.

    - They have dimensions and a transform in Unity, as well as a specific real-world size.

    - They can be repositioned, but people cannot resize them.

    - The dimensions and the transform of the volume camera define the region of your scene that your app will display in a volume.

    - They're specified in scene units.

    - You can see a preview of the volume in green in Unity's scene view.

    - By manipulating the dimensions and the transform of the volume camera, different parts of the scene can be brought into the volume.

    - If I move or rotate the camera, new objects become visible in my space.

    - If I scale up its size, more of the scene comes into view.

    - In both cases, the volume remains the same size.

    - Only the content visible inside of it changes.

        - Notice that in the initial placement of the volume camera, the spring intersects the side of the volume; content is clipped by RealityKit.

        - If you will have content intersecting the edges of your volume, consider placing the same mesh in your scene a second time with a back-facing material to fill in the clipped sections.

- Your unbounded volume displays in a full space on this platform and allows your content to fully blend with passthrough for a more immersive experience.

    - It has no dimensions because it selects your entire scene, and its transform specifies how your scene units are mapped to real-world units.

    - There can only be one unbounded volume camera active at a time.

    - You'll see an example of an unbounded volume when we talk about interaction.

####  Build interaction
- Unity supports multiple input types for apps on this platform.

    - On this platform, people use their eyes and hands to look at content and tap their fingers together to select it.

        - Full hand tracking as well as head pose data lets you create realistic interactions.

        - Augmented reality data from ARKit is available, as are Bluetooth devices such as keyboards and game controllers.

        - The tap gesture is the most common way of interacting with content on this platform.

    - In order for your objects to receive these events, they must have input colliders configured.

    - You can look and tap to select an object from a distance, or you can reach out and directly touch an object with a finger.

    - Up to two simultaneous tap actions can be in progress.

- In Unity, taps are available as WorldTouch events.

    - They are similar to 2D tap events, but have a full 3D position.

    - Hand and head pose tracking gives your application precise information about each hand joint and the viewer's head position relative to the global tracking origin.

    - Low-level hand data is provided via Unity's Hands package, and head pose is provided through the Input System.

    - Both of these are available in unbounded volumes only, and accessing hand tracking requires your application to request permission to receive the data.

    - Augmented reality data such as detected planes, the world mesh, and image markers are available through ARKit and Unity's AR Foundation.

        - Like hands and head pose, AR data is only available in unbounded volumes and requires extra permissions.

        - Finally, Bluetooth devices such as keyboards, controllers, and other supported devices are available for you to access through Unity's Input System.

- Because some types of input are only available in unbounded volumes, you'll need to decide what type of interaction you would like to build.

    - Using look and tap will allow your content to work in a bounded volume that can live alongside other applications, but if you need access to hand tracking or augmented reality data, you'll need to use an unbounded volume and request permissions.

    - Each of these is delivered to your Unity application via an appropriate mechanism.

        - This sample uses tapping, hand tracking, and plane detection in an unbounded volume scene.

        - You can look at a surface found via ARKit plane detection and create flowers by dragging your finger along it.

        - The flowers are painted using hand tracking, and you can tap to grow flowers.

        - Flowers that you grow react to hand movement using Unity's physics system.

    - By incorporating the real world into your content in this way, you can create a much deeper sense of immersion.

- The best way to adapt your existing interactions depends on the type.

    - If you are already working with touch, such as on an iPhone, you can add appropriate input colliders and continue to use tap as your primary input mechanism.

    - If you are using VR controllers, you will have to redefine your interactions in terms of either tap or hand-based input, depending on how complex they are.

    - Existing hand-based input should work without changes.

- And if you have existing UI panels using one of Unity's UI systems, you can bring them to this platform.
- User interface elements built using uGUI, as well as UI Toolkit, are supported.

- If you are using other UI systems, they will work as long as they use meshes and MeshRenderers or draw to a RenderTexture, which is then placed on a mesh.

#### Prepare for the platform
 
- Support for spatial computing on Apple platforms will be coming soon in beta based on Unity 2022.

    - If you're starting a new project, use Unity 2022 or later.

    - If you have an existing project, start upgrading to 2022.

    - If you have handwritten shaders in your project, start converting them to Shader Graph.

- Consider adopting the Universal Render Pipeline.

    - While the built-in graphics pipeline is supported, all future improvements will be on the Universal pipeline.

- If you haven't yet, start using the Input System package.

- Mixed-mode input is supported, but platform events are only delivered through the Input System.

- Finally, start thinking about how you can bring an existing app or game to spatial computing, or what new experience you'd like to create.

    - Consider whether your idea fits in the shared space to give people more flexibility, or if your app needs the power of a full space.

- To get more information about Unity's support for this platform, and to sign up for early beta access, please visit unity.com/spatial.

- For more 
    - ["Bring your Unity VR app to a fully immersive space.](https://developer.apple.com/videos/play/wwdc2023/10093)
    - ["Build great games for spatial computing"](https://developer.apple.com/videos/play/wwdc2023/10096) to get an overview of game development technologies for this platform.
