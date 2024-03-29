---
title: Create 3D models for Quick Look spatial experiences
---

### [Create 3D models for Quick Look spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10274/)

The next step Apple suggest is to learn about the Quick Look on VisionOS, lets check out how Quick Look adds powerful previews for 3D content.

"Discover best practices when creating 3D content for Quick Look on visionOS. We'll explore a few different ways to prepare your models for Quick Look, cover important considerations for 3D quality and performance, and show you how to use Reality Composer Pro and Reality Trace to inspect and fine-tune your content."
-Apple

#### Overview
- Today, I will walk you through how to create the 3D models for Quick Look spatial experiences.

- Before we get into that, see [[Discover Quick Look for spatial computing]] we have shown you this lovely 3D model of a room that we have created using our new Room Plan API.

    - We brought this model into Quick Look by just dragging a USDZ file out from our application window, which opens up a Quick Look preview right where we dropped it.

    - From here, you can start to interact with Quick Look and my content by using familiar gestures.

- Before we dive deeper into the story behind this model, let's talk a bit more about how the system presents 3D content in Quick Look.

    - On this platform, Quick Look displays a 3D model in a volume window.

    - Volume windows have defined bounds to allow sharing them alongside with other apps.

    - People can reposition volumes in space and they can view it from different angles.

    - 3D models are always placed at the center of the volume.

        - When the model first appears, Quick Look will orient the volume window so that the content is directly facing you.

        - From here, you can use the volume window bar below the 3D model to reposition content freely in your space.

        - Quick Look will automatically adjust the size of the volume based on how people scale the model when they are in a preview session.

        - It's important to note that if your content is using animations, we suggest keeping all animations to be inside the defined bounds of the Quick Look volume.

- We just covered the basics of how Quick Look presents your 3D content.

    - There are additional considerations when it comes to how Quick Look is using model size and scale.

    - When loading the 3D model, Quick Look will respect the metersPerUnit defined in the USDZ's metadata to determine the scale unit with respect to the real world.

    - In order to help people visualize the scale of the assets, Quick Look will try to present the model initially at a 100 percent scale if it is authored to be within a certain size range.

    - Let's see an example.

        - Quick Look imposes a minimum scale to ensure that you can enjoy all content, even when it came at a tiny scale, such as this tin car.

        - Quick Look is also using an upper bound limit in case you are viewing very large objects to ensure they are not occupying too much space alongside your other apps.

        - For any objects with a size in between, such as this teapot, Quick Look will use a model's real-world size when initially launched in space.

- Remember, you can always view models at their real-world size by tapping on the button below your volume window.

    - Now that we know how Quick Look handles the size of your model, let's look at two more things that Quick Look adds when it presents your content: ground plane and shadows.

    - Quick Look will automatically show a ground plane and shadow below your model to give you a better understanding of the model's size and its position relative to the ground.

    - Because Quick Look is doing this work for you, we suggest that you do not add your own ground plane and shadows for your model.

- So far, we covered the basics of how Quick Look will show your 3D content.

    - Let's walk you through the agenda for the remainder of this session.

    - First, we will look into a few ways to create 3D models.

    - Next, we will talk about how you can inspect the visual quality of your content and make adjustments as needed.

    - Lastly, we will cover how to make sure your 3D content can render and run with great performance.

##### Model creation

- Let's get started with preparing your 3D content.

- Quick Look accepts USDZ as its primary format to handle 3D models.

    - USDZ is at the heart of 3D content for Apple platforms and designed to be lightweight and optimized for shade.

- Let's take a look at how you can create USDZ files.

- There are many ways to create a USDZ file.

    - First, if you have previously created a USDZ file for iOS, you can use the same file for Quick Look on this new platform.

        - In case you want to create a new USDZ file from scratch, you can use professional digital content creation tools to create 3D content and then export out as a USDZ file.

    - You can also scan 3D models and create a USDZ file of real-world objects by using our RealityKit Object Capture API.

        - Object Capture provides you with an end-to-end photogrammetry solution along with sample apps to help you create 3D models at different detail levels.

        - Object Capture is supported on both iOS and macOS devices.

    - Finally, if you're looking for a way to create a 2D or 3D floor plan over your house, we have you covered with our RoomPlan API.

        - Remember how I mentioned there is a backstory to the 3D room model I showed you earlier? Let's dive into the workflow that our 3D designer, Jerry, has used to create this 3D model.

        - First, Jerry starts to scan his room by using RoomPlan sample application.

        - After only a short time, he can preview the 3D layout of his room, or export and drop a USDZ file right to his Mac.

        - Next, Jerry imports the 3D model into a 3D content creation tool to bring his design concepts to life.

        - Here is the result of that work.

        - This model looks great.

        - You can see some materials and textures got added to walls, floor, and some other room elements.

        - Now, the room model that Jerry created is almost ready to preview in Quick Look.


#### Visual quality
- Luckily, there is a new tool called Reality Composer Pro that makes this next step really easy.

    - Previewing your 3D models for Quick Look is a really important step in your content creation workflow to inspect the real-world quality of your model and make adjustments as needed.

    - Let's take a closer look.

    - Here is the Reality Composer Pro with our 3D model loaded in the main view.

    - By simply clicking on this button located at the top-right corner in Reality Composer Pro, you can easily preview your 3D model in Quick Look right on your device.

    - And here is the same 3D model running in Quick Look.

    - One thing we can notice now is that the initial model orientation does not look right.

    - As previously discussed, it is important to ensure that the most interesting part of the 3D model is presented facing towards you to create an engaging experience.

    - Let's see how we can fix this.

        - Quick Look is using a right-hand coordinate system.

        - Knowing this, we can easily fix the orientation of our 3D model in our content creation tool, or right here in Reality Composer Pro.

        - In our case, we need to rotate the model on the vertical axis so that the living room in our model comes into view.

        - You can fix this by putting 90 degrees around y-axis here, just like this.
        <img src="/assets/Step_Ten_VisionOS_Assets/BuildQuicklook1.png"/>
        - Let's again use device preview from Reality Composer Pro to check out the changes to our model.

        - Now the orientation is fixed, and we have a much better view on this great looking model.

        - OK, let's explore this asset even further, and get a different perspective and see a few more details here.

        - To do so, you can use a pinch and drag gesture to rotate the 3D model and view it from different sides.

        - This gives me a really good view on the different parts of our room.

        - You can also use a two-hand pinch gesture to scale the model and see more details.

- Now that we have seen how to inspect your 3D model in Quick Look on device, let's talk about a few considerations for enhancing the visual quality of your content.

    - When multiple objects are rendered in same location, they can overlap and appear as a single flickering object.

        - To reduce this problem, you can use 3D creation tools to optimize the mesh geometry either by removing the overlap or increasing the distance between the flickering objects.

    - Try to avoid using high-frequency normal maps, since they remain results in aliasing issues that can create unwanted visual artifacts, especially in situations where you are in motion or up close to the 3D model.

    - When rendering a small or thin object such as leaves, the system may not be consistently sampled over time under variable rasterization rates, which may cause flickering in the periphery.

        - To minimize this issue, you can try storing the fine geometry details into an opacity texture and then render it by using a geometry with a larger triangle grid instead.

        - To learn more about variable rasterization rates check out our session, [[Explore rendering for spatial computing]] Next, let's turn our attention to performance.


#### Performance
- Here, we will look into the anatomy of Quick Look 3D content and what you can do to ensure a smooth and seamless QuickLook spatial experience.

- There are many factors that determine the 3D performance of your content that gets rendered in Quick Look.

    - Things like what's the file size of your 3D model, or 
    - the count and resolution of textures, or 
    - even the complexity of materials that you are using for your model.

- In order to know where to start optimizing your 3D model for performance, you need to first identify potential limitations that might exist with your asset.

    - To help simplify this task, we have introduced some helpful new tools this year, which can significantly improve your workflow.

###### Tools for Performance
- Here, we are back in Reality Composer Pro to show you the Statistics panel.

    - This panel provides you with a lot of helpful information about your 3D model characteristics, such as the number of triangles and the amount of texture memory being used with your content.

- Another great tool at your disposal is RealityKit Trace.

    - This tool allows for even more advanced runtime profiling.

    - RealityKit Trace provides insights into specific rendering pipeline.

    - It allows you to get more information into the individual rendering frames with your 3D content.

    - By analyzing several captured frames, RealityKit Trace can be used to identify and diagnose potential performance issues or limitations, and give you recommendations.

    - RealityKit Trace keeps building with Xcode.

    - To use it for profiling your content in Quick Look, you need to attach it to the Quick Look process.

    - For more details
        -  [[Meet Reality Composer Pro]] 
        -  [[Meet RealityKit Trace]]

##### Performance Optimizations
- Now that we have looked at some of the tools to help you do profiling for potential performance limitations, let's go over some of the best practices to help you optimize 3D content for performance.

- Earlier, I mentioned the different factors that determines the performance of Quick Look's 3D content.

- Now, let's look at those one by one from the perspective of what you can do to optimize content accordingly.

    - First up is optimizing your model for file size.

        - Smaller file size usually results in quicker downloads and faster loading time, as you don't want the user to wait a long time before interacting with your content.

        - The trick here is try to find an optimized balance between asset quality and file size.

        - For instance, you could use less detailed textures or lower-quality audio sources.

        - Sometimes, assets are developed over several iteration cycles.

        - Oftentimes, this includes changes to underlying audio, animations, and textures linked to your assets.

        - To keep file size to a minimum, make sure to only include what's really used in the final package that gets distributed.

            - For example, older versions of audio files that are no longer being used for your scene should be removed from final assets before distribution.

        - Lastly, to ensure a better sharing experience, we recommend you keep your file size less than 25 megabytes.

    - Next, let's look into how to optimize your 3D content geometry for performance.

        - Again, the trick is to find the right balance between showing great level of details and achieving great performance.

        - In case your model is using parts that are hidden or fully covered by another geometry, meaning they are never shown on the screen, it's OK to remove them to save on your performance budget.

        - Also, consider merging small meshes into a single larger one to reduce system loads.

        - For a single model, we recommend that you keep it under 200 mesh parts and fewer than 100k vertices.

        - Always keep in mind to balance your mesh detail with another asset in the scene.

    - Next, let's look at textures.

        - Texture can contribute to a lot of memory usage.

        - Automized textures consume less memory, which allows more assets to be loaded at the same time and helps complex scenes run smoothly.

        - One way to save on texture budget is by using grayscale for your noncolor inputs.

        - In some cases, you can even pack your grayscale images into individual channels over a color texture, allowing you to store multiple grayscale maps into a single texture.

        - When possible, use constant values in your materials instead of loading them from texture.

        - If your model is only using a single PBR material, we recommend a maximum texture size of 2K by 2K and using 8-bit instead of 16-bit per channel textures.

        - Finally, be sure to always spend your texture budget in areas that add most value and realism for your 3D model.

    - Next up is materials.

        - Materials define the surface properties of a 3D model.

        - They specify how the system renders the model, including its color and whether your object appears with a shiny or reflective look.

        - When it comes to optimizing your materials for 3D models, you can reduce your loading time by combining mesh parts to share with the same material.

        - The reason this helps is because when your 3D model has custom materials, the system has to compile them when it loads for the first time.

        - Be sure to balance your material's complexity against the screen size.

            - For example, if you just need a tiny part of the screen to be transparent or have clear coat, it's more efficient to use a separate material just for that small area.

        - You always need to be mindful of overlapping transparency.

            - Rendering transparent objects in real time typically requires more calculations compared to the opaque ones, so only have overlapping transparency when you really need it.

        - Also, if you have baked lighting or some parts of your mesh do not even need lighting, we recommend using MaterialX Unlit surface to save real-time lighting computation.

    - Next, let's look into physics.

        - Physics simulation sometimes can be computationally expensive, especially in cases where the physics system performs collision detection and simulates realistic effects, like gravity and springs.

        - To maximize your content performance by using physics, you can try to reduce the total number of colliders being used.

        - Sometimes you want your content to participate in physics simulation, but then your content includes entities that are not supposed to move or be affected by another object -- for example, a wall that will make a virtual ball bounce off.

        - In this case, we recommend using static colliders to reduce physics computations.

    - Next, let's talk about animation.

        - Adding animations to your 3D models is a great way to bring your content to life.

        - Sometimes, all you need is just an idle animation.

        - In this case, limit the number of weight per vertex for your animation to help create efficient and realistic animations.

        - When you are trying to optimize geometry of your deformations or skinned animations, remember to follow the same geometry guidelines I provided previously.

    - Next up is using particle systems with your content.

        - This is one of the most powerful tools for building sophisticated visual effects such such as realistic fire with smoke or exhaust from a rocket.

        - If used incorrectly, particles can be a bottleneck in your Quick Look 3D experience.

        - For this reason, we suggest you limit your usage of particle emitters and keep the number of onscreen particles to a minimum.

        - Often, you can create similar visual effects with fewer particles.

        - Experiment with simpler or smaller shapes and styles to achieve a similar effect, which will help reduce overdraw on the system.

#### Conclusion
- That was quite a number of things we just went through.

- Let's summarize those recommendations for you.

    - There are many factors that count into performance of your Quicklook 3D content.

    - This new platform has been designed to let people engage with multiple apps and pieces of content that are running alongside each other.

    - This means that the performance of your content may even be impacted by other apps or scenes that people are doing.

    - For this reason, it's good practice to test your 3D model across different scenarios.

    - As I have shared in this session, there are a number of tools available at your disposal, whether you want to check the visual quality of your content or find limitations that could impact your 3D performance.

    - The sweet spot here is to find the right balance between having greater visuals and ensuring a smooth Quick Look viewing experience at the same time.
