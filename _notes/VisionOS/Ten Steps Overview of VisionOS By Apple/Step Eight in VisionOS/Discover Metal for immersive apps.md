---
title: Discover Metal for immersive apps
---

### [Discover Metal for immersive apps](https://developer.apple.com/videos/play/wwdc2023/10089/)

The next step Apple suggest is to learn about the Metal, lets check out when and where we should use Metal.

"Find out how you can use Metal to render fully immersive experiences for visionOS. We'll show you how to set up a rendering session on the platform and create a basic render loop, and share how you can make your experience interactive by incorporating spatial input."
-Apple

#### Intro
When creating fully immersive experiences, you have a few choices when it comes to your rendering method.

You can still use RealityKit, or if you prefer, you can choose Metal and ARKit APIs.

RecRoom is a great example of an application that provides a fully immersive experience using CompositorServices to create a rendering session, Metal APIs to render frames, and ARKit to get world and hand tracking.

They were able to bring support to all these technologies thanks to the Unity editor.

If you'd like to write your own engine, the CompositorServices API gives you access to Metal rendering on xrOS.

You can combine it with ARKit, which adds world tracking and hand tracking, to create a fully immersive experience.

CompositorServices is the key to configure your engine to work on xrOS.

I'll show you how to setup the render loop and then how to render one frame.

Finally, I'll show you how to use ARKit to make your experience interactive.

#### App Architecture
- Start with the architecture of an xrOS app.

- You'll get the most out of today's session if you have previous experience with Metal APIs and Metal rendering techniques.

    - If you haven't used Metal before, check out the code samples and documentation over in developer.apple.com/Metal.

- When you create immersive experiences on xrOS with Metal, you'll start with SwiftUI to create the application and the rendering session.

- After creating the rendering session, you can switch to a language you might be more familiar with, like C or C++, to define the inner parts of the engine.

- You start by creating a type that conforms to the SwiftUI app protocol.

    - To conform to this protocol, you will define the list of scenes in your app.

        - On xrOS, there are three main scenes types.

        - The window type provides an experience similar to 2D platforms like macOS.

        - The volume type renders content within its bounds and it coexists in the Shared Space with other applications.

        - And ImmersiveSpace allows you to render content anywhere.

- Whenever you render fully immersive experiences with Metal, you will choose the ImmersiveSpace type.

    - ImmersiveSpace is a new SwiftUI Scene type available on xrOS.

        - It serves as the container for fully immersive experiences.

        - To learn how to use ImmersiveSpace, check out the session [[Go beyond the window with SwiftUI]] 
        - When you create an ImmersiveSpace scene, your application provides the content by using a type that conforms to the ImmersiveSpaceContent protocol.

        - Often, when creating content for an ImmersiveSpace Scene, applications will use RealityKit.

            - It uses CoreAnimation and MaterialX under the hood.

            - But if instead, you'd like to use the power of Metal to render the content of your application, you've got another option.

            - The CompositorServices API uses Metal and ARKit to provide immersive rendering capabilities to your application.

    - The new CompositorServices API, introduced in xrOS, provides a Metal rendering interface to be able to render the contents of an ImmersiveSpace.

        - With CompositorServices, applications can render directly into the compositor server.

        - It has a low IPC overhead to minimize latency, and it is built from the ground up to support both C and Swift APIs.

        - When using CompositorServices, the ImmersiveSpaceContent is called CompositorLayer.

        - To create a CompositorLayer you will need to provide two parameters.

            - The first one is the CompositorLayerConfiguration protocol.

                - This protocol defines the behavior and capabilities of your rendering session.

            - The second is the LayerRenderer.

                - This is the interface to the layer rendering session.

        - Your application will use this object to schedule and render new frames.

            - When writing an immersive experience with Metal, start by defining the app type.

                - As the scene type, use ImmersiveSpace.

                - For the content type, use a CompositorLayer.

        - Once the CompositorLayer is ready to render content, the system will call the application with the instance of the rendering session.

        - Here is a good place to create the instance of your custom engine.
        ```
        @main
        struct MyApp: App {
            var body: some Scene {
                ImmersiveSpace {
                    CompositorLayer { layerRenderer in
                        let engine = my_engine_create(layerRenderer)
                        let renderThread = Thread {
                            my_engine_render_loop(engine)
                        }
                        renderThread.name = "Render Thread"
                        renderThread.start()
                    }
                }
            }
        }
        ```
        - Now that you have the engine instance, you can create the render thread and run the render loop by calling start.

        - One thing to take into account when defining the scene list in your application, is that by default SwiftUI creates a window scene, even if the first scene in your app is an ImmersiveSpace.

            - To change that default behavior, you can modify the info plist of your app.

            - You can add the key UIApplicationPreferred DefaultSceneSessionRole to your application scene manifest to change the default scene type of your application.

            - If you are using a space with a Compositor SpaceContent, you will use CPSceneSessionRole ImmersiveSpaceApplication.

            - After setting up the application, and before getting in the render loop, you'll tell CompositorServices how to configure the LayerRenderer.

#### Render configuration
- To provide a configuration to the CompositorLayer, you will create a new type that conforms to the CompositorLayerConfiguration protocol.

    - This protocol allows you to modify the setup and some of the behavior of the rendering session.

    - The CompositorLayerConfiguration provides you two parameters.

        - The first one is the layer capabilities.

            - It enables you to query what features are available on the device.

            - Use the capabilities to create a valid configuration.

        - And the second parameter is the LayerRenderer Configuration.

            - This type defines the configuration of your rendering session.

            - With the configuration, you can define how your engine maps its content into the layer, enable foveated rendering, and define the color management of your pipeline.

- Now, I'll talk about how each of these properties will affect your engine.

    - The first one is foveated rendering.

        - The main goal of this feature is to allow you to render content at a higher pixel-per-degree density without using a bigger texture size.

        - In a regular display pipeline, the pixels are distributed linearly in a texture.

        - xrOS optimizes this workflow by creating a map that defines what regions in a display can use a lower sampling rate.

            - This helps reduce the power required to render your frame while maintaining the visual fidelity of the display.

        - Using foveation whenever possible is important, as it will result in a better visual experience.

        - A great way to visualize how foveation affects your rendering pipeline is using Xcode's Metal Debugger.

        - With Metal Debugger, you can inspect the target textures and rasterization rate maps being used in the render pipeline.

            - This capture shows the contents of the texture without scaling for the rasterization rate map.

            - You can notice the different sample rates by focusing in the regions of the texture that are more compressed.

            - With the attachment viewer options in Metal Debugger, you can scale the image to visualize the final result that the display will show.

        - Compositor provides the foveation map using an MTLRasterizationRateMap for each frame.

        - It is a good practice to always check if foveation is supported.

        - This will change depending on the platform.

        - For example, in the xrOS simulator, foveation is not available.

        - To enable foveation, you can set isFoveationEnabled on the configuration.

    - The second property is LayerRenderer layout.

        - This property is one of the most important configurations for your engine.

        - It defines how each display from the headset gets mapped into the rendered content of your application.

            - Each eye first maps into a Metal texture provided by Compositor.

            - Then Compositor provides the index of which slice to use within that texture.

            - And finally, Compositor provides the viewport to use within that texture slice.

        - The LayerRenderer layout lets you choose different mappings between the texture slice and viewport.

            - With layered, Compositor will use one texture with two slices and two viewports.

            - With dedicated, Compositor will use two textures with one slice and one viewport each.

            - And finally with shared, Compositor will use one texture, one slice, and two different viewports for that slice.

        - Choosing which layout to use will depend on how you set up your rendering pipeline.

            - For example, with layered and shared, you will be able to perform your rendering in one single pass, so you can optimize your rendering pipeline.

        - With shared layout, it might be easier to port existing code bases where foveated rendering is not an option.

        - Layered layout is the optimal layout since it allows you to render your scene in a single pass while still maintaining foveated rendering.

    - The last configuration property to discuss is color management.

        - Compositor expects the content to be rendered with extended linear display P3 color space.

    - xrOS supports an EDR headroom of 2.0.

        - That is two times the SDR range.

    - By default, Compositor does not use a pixel format that is HDR renderable, but if your application supports HDR, you can specify rgba16Float in the layer configuration.

        - If you want to know more about how to render HDR with EDR, checkout the session [Explore HDR rendering with EDR](https://developer.apple.com/videos/play/wwdc2021/10161) 
    - To create a custom configuration in your application, start by defining a new type that conforms to the CompositorLayerConfiguration protocol.

        - To conform to this protocol, add the makeConfiguration method.

            - This method provides the layer capabilities and a configuration you can modify.

        - To enable the three properties I mentioned before, first check if foveation is supported.

        - Then check what layouts are supported in this device.

        - With this information, you can set a valid layout in the configuration.

        - In some devices like the simulator, where the Compositor only renders one view, layered won't be available.

        - For foveation, set it to true if the device supports it.

        - And finally, set the colorFormat to rgba16Float to be able to render HDR content.

    - Returning to the code that created the Compositor layer, you can now add the configuration type you just created.
```
// CompositorLayer configuration

struct MyConfiguration: CompositorLayerConfiguration {
    func makeConfiguration(capabilities: LayerRenderer.Capabilities,
                           configuration: inout LayerRenderer.Configuration) {

        let supportsFoveation = capabilities.supportsFoveation
        let supportedLayouts = capabilities.supportedLayouts(options: supportsFoveation ?
                                                             [.foveationEnabled] : [])

        configuration.layout = supportedLayouts.contains(.layered) ? .layered : .dedicated

        configuration.isFoveationEnabled = supportsFoveation

        // HDR support
        configuration.colorFormat = .rgba16Float
   }
}
```

#### Render Loop
- Now that the rendering session is configured, you can set up the render loop.

- You'll start by using the LayerRenderer object from the CompositorLayer.

    - First, you'll load the resources and initialize any objects that your engine will need to render frames.

    - Then check the state of the layer.

        - If the layer is paused, wait until the layer is running.

    - Once the layer is unblocked from the wait, check the layer state again.

        - If the layer is running, you'll be able to render a frame.

        - And once that frame is rendered, check the layer state again before rendering the next frame.

        - If the layer state is invalidated, free the resources you created for the render loop.

- Now, it's time to define the main function of the render_loop.

    - Until now I've been using Swift since the ImmersiveSpace API is only available in Swift.

    - But from here I will switch to C to write the render loop.
```
void my_engine_render_loop(my_engine *engine) {
    my_engine_setup_render_pipeline(engine);

    bool is_rendering = true;
    while (is_rendering) @autoreleasepool {
        switch (cp_layer_renderer_get_state(engine->layer_renderer)) {
            case cp_layer_renderer_state_paused:
                cp_layer_renderer_wait_until_running(engine->layer_renderer);
                break;
            case cp_layer_renderer_state_running:
                my_engine_render_new_frame(engine);
                break;
            case cp_layer_renderer_state_invalidated:
                is_rendering = false;
                break;
        }
    }

    my_engine_invalidate(engine);
}
```
- As I mentioned, the first step in the render loop is to allocate and initialize all the objects you'll need to render frames.

    - You'll do this by calling the setup function in your custom engine.

    - Next, is the main section of the loop.

    - The first step is to check the layerRenderer state.

        - If the state is paused, the thread will sleep until the layerRenderer is running.

        - If the layer state is running, the engine will render one frame.

        - And finally, if the layer has been invalidated, the render loop will finish.

    - The last step of the render_loop function will be to clear any used resources.

#### Render a frame
- Now that the app is going through the render loop, I'll explain how to render one frame.

- Rendering content in xrOS is always from the point of view of the device.

- You can use ARKit to obtain the device orientation and translation.

- ARKit is already available on iOS, and now xrOS is introducing a whole new API, which has additional features that can help you create immersive experiences.

    - With ARKit, you can add world tracking, hand tracking, and other world sensing capabilities to your application.

    - The new ARKit API is also built from the ground up to support C and Swift APIs, which will allow for an easier integration with existing rendering engines.

        - To learn more about ARKit on xrOS, check out [[Meet ARKit for spatial computing]] Within the render loop, it's time to render one frame.


- When rendering a frame, Compositor defines two main sections.

    - The first one is the update.

        - Here's where you will do any work that is not input-latency critical.

        - This can be things like updating the animations in your scene, updating your characters, or gathering inputs in your system like hand skeleton poses.

    - The second section of the frame is the submission section.

        - Here's where you will perform any latency-critical work.

        - You'll also render any content that is headset-pose dependent here.

    - In order to define the timing for each of those sections, Compositor provides a timing object.

        - This diagram defines how the timing affects the different frame sections.

            - The CPU and GPU tracks represent the work that is being done by your application.

            - And the Compositor track represents the work done by the Compositor server to display your frame.

            - The timing type from Compositor Services defines three main time values.

                - First is the optimal input time.

                    - That is the best time to query the latency-critical input and start rendering your frame.

                - Second is the rendering deadline.

                    - That is the time by when your CPU and GPU work to render a frame should be finished.

                - And third is presentation time.

                    - That is the time when your frame will be presented on display.

- In the two sections of your frame, The update section should happen before the optimal input time.

    - After the update, you will wait for the optimal input time before starting the frame submission.

- Then you will perform the frame submission, which will submit the render work to the GPU.

    - It is important to notice that the CPU and GPU work needs to finish before the rendering deadline, otherwise the Compositor server won't be able to use this frame and will use a previous one instead.

- Finally, on the rendering deadline, the Compositor server will composite this frame with the other layers in the system.

<img src="/assets/Step_Eight_VisionOS_Assets/MetalCompositerDiagram.png"/>

- Back to the render loop code, it's time to define the render_new_frame function.
```
void my_engine_render_new_frame(my_engine *engine) {
    
    cp_frame_t frame = cp_layer_renderer_query_next_frame(engine->layer_renderer);
    if (frame == nullptr) { return; }
    
    cp_frame_timing_t timing = cp_frame_predict_timing(frame);
    if (timing == nullptr) { return; }

    cp_frame_start_update(frame);

    my_input_state input_state = my_engine_gather_inputs(engine, timing);
    my_engine_update_frame(engine, timing, input_state);

    cp_frame_end_update(frame);

    // Wait until the optimal time for querying the input
    cp_time_wait_until(cp_frame_timing_get_optimal_input_time(timing));

    cp_frame_start_submission(frame);

    cp_drawable_t drawable = cp_frame_query_drawable(frame);
    if (drawable == nullptr) { return; }

    cp_frame_timing_t final_timing = cp_drawable_get_frame_timing(drawable);
    ar_pose_t pose = my_engine_get_ar_pose(engine, final_timing);
    cp_drawable_set_ar_pose(drawable, pose);

    my_engine_draw_and_submit_frame(engine, frame, drawable);

    cp_frame_end_submission(frame);
}
```
- In your engine's render_new_frame function, you will first query a frame from the layerRenderer.

- With the frame object, you will be able to predict the timing information.

    - Use that timing information to scope the update and submit intervals.

- Next, implement the update section.

    - Define this section by calling the start and end update on the frame.

    - Inside, you will gather the device inputs and update the contents of the frame.

- Once the update is finished, wait for the optimal input time before starting the submission.

    - After the wait, define the submission section by calling start and end submission.

        - Inside this section, first query the drawable object.

        - Similar to CAMetalLayer, the drawable object contains the target texture and the information that you will need to set up the render pipeline.

- Now that you have your drawable, you can get the final timing information that Compositor will use to render this frame.

    - With the final timing, you can query the ar_pose.

    - It is important to set the pose in the drawable since it will be used by the Compositor to perform reprojection on the frame.

    - Here I'm getting the pose by calling the get_ar_pose function in my engine object.

        - But you will need to implement the contents of this function using the ARKit world tracking APIs.

- The last step of the function will be to encode all the GPU work and submit the frame.

    - Inside the submit_frame, use the drawable to render the contents of the frame as usual.

    - Now that the render loop is rendering frames, it's time to make your immersive experience interactive.

#### User input
- This video shows how RecRoom using Unity is already taking advantage of the ARKit and Compositor APIs to add interactivity to their application.

- There are two main input sources driving this interaction.

    - ARKit's HandTracking is providing the hand skeleton to render virtual hands.

    - And pinch events from the LayerRenderer are driving the user interactions.

- In order to make the experience interactive, you'll first gather the user input and then apply it to the contents of your scene.

    - All this work will happen in the update section of the frame.

- There are two main input sources, the LayerRenderer and the ARKit HandTracking provider.

    - With the LayerRenderer, you will get updates every time the application receives a pinch event.

        - These updates are exposed in the form of spatial events.

        - These events contains three main properties.

            - The phase will tell you if the event is active, if it finished, or if it got canceled.

            - The selection ray will allow you to determine the content of the scene that had the attention when the event began.

            - And the last event property is the manipulator pose.

                - This is the pose of the pinch and gets updated every frame for the duration of the event.

    - From the HandTracking API, you will be able to get skeleton for both the left and right hands.

- Now, it's time to add input support in the code.

    - Before gathering the input, you will decide if your application is rendering virtual hands or if it uses passthrough hands.

    - Add the upperLimbVisibility scene modifier to the ImmersiveSpace to make the passthrough hands visible or hidden.

        - To access the spatial events, go back to where you defined the CompositorLayer render handler.

        - Here, register a block in the layerRenderer to get updates every time there is a new spatial event.

            - If you are writing your engine code in C, you'll map the SwiftUI spatial event to a C type.

            - Inside the C code, you can now receive the C event collection.

- One thing to keep in mind when handling the spatial event updates is that the updates get delivered in the main thread.

    - This means that you will use some synchronization mechanism when reading and writing the events in your engine.

- Now that the events are stored in the engine, it's time to implement the gather input function.

    - The first step is to create an object to store the current input state for this frame.

    - This input state will store the events that you received from the LayerRenderer.

        - Make sure that you are accessing your internal storage in a safe way.

- As for the hand skeleton, you can use the hand tracking provider API from ARKit to get the latest hand anchors.

    - And now that your application has input support, you have all the tools at your disposal to create fully immersive experiences on xrOS.

