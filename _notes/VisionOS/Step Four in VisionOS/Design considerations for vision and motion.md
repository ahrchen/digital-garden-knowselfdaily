---
title: Design considerations for vision and motion
---

### [Design considerations for vision and motion](https://developer.apple.com/videos/play/wwdc2023/10078/)

This video provides several key tips on good vision and motion. Design engaging immersive experiences for visionOS that respect the limitations of human vision and motion perception. We'll show you how you can use depth cues, contrast, focus, and motion to keep people comfortable as they enjoy your apps and games.


#### Visual depth cues

- Your content needs to give the viewer the right visual depth clues, as well-designed 3D content helps the brain to perceive depth
    - Vision comfort requires agreement between the depth intended by you and the depth perceived by the viewer
    - The brain relies on the eye muscles to converge the line of sight and fixate the eyes at the image depth to perceive a single image.
        -  it needs correct visual depth cues to converge the eyes correctly
        -  ![](https://www.wwdcnotes.com/images/notes/wwdc23/10078/Eyes_Converge.jpeg)
- How to use image cues to maintain vision comfort
    - Color perception helps us recognize familiar size cues from previous experiences.
    - Blur gives a sense of depth
    - The relative size of an image can be used to provide depth information. The larger is the closer.
    - Gentle motion can help to figure out how far away you need to look.
    - Missing visual depth cues can be added with a background, light and shadow, occlusion, and texture density
- The more conflicting cues, suggest more vision discomfort
    - Correct visual cues that can be confusing, like repeating patterns
    - You can avoid double vision by using smaller pieces of the pattern or breaking up the pattern with another design
    - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10078/Patterns.jpeg)

- Warning If you decide to create stereo video content manually, it is extremely important to have the correct depth cues and also the correct disparity for each eye
- <img src="/assets/Manual_stereo_video_content_cues.png"/>


#### Content parameters

- Parameters that reduce effort 

    - Depth
        - Content that requires the eyes to be fixed for a long time, like reading, is most comfortable when it is placed farther than arms-length distance
        - Allow the content depth to be adjusted
        - Reserve content closest to the viewer for momentary visual effort experiences or for inviting direct interaction
        - Use visual cues, transparency/blur 
        
    - Size and contrast
        - Content size and contrast should match the particular visual experience you are designing to allow for vision comfort For example:
            - Higher contrast for reading text
            - Lower contrast, transparency, or blur to redirect visual attention elsewhere
            - Choose the right font size, window size, and depth for long reading. Doing this will make it easy to read without having to move your head or body
            - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10078/Font_Window_Size.png)
        - When a large portion of the field of view is dark, slow down the transition to a bright scene to give time to the eye for brightness adaptation


#### Eye effort

- Minimize Eye Comfort 
    - Position
        - It's most comfortable for people to look downwards or left and right
        - Upward and diagonal eye rotation takes the most eye-muscle effort
        - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10078/Eye_Effort.jpeg)

    - Reading
        - Content requiring extended reading or elongated target fixations should be placed towards the center and slightly below line of sight
        
    - Reduce eye rotation
        - Center the objects
        - Minimize time needed for eye rotation
        - Design for natural breaks in your experience to allow the person's eyes to rest

#### Motion of virtual objects

- You might feel motion discomfort like dizziness or an upset stomach when the visual system information doesn't match the vestibular system

    - Note > Well-designed content enables the brain to perceive the world as stationary
        - Providing a sense of stability

- When virtual objects, cover a large part of the field of view and move, the viewer's brain might interpret the visual motion of the objects as if the viewer themself is moving
    - This upsets the vestibular system, because you feel like you are moving visually, but the vestibular system does not.
    - Resolve by making the objects semitransparent when they move, so the passthrough content is clearly visible during the motion

#### Head-locked content

**Warning** When possible, avoid content that is anchored to the user's head

- If head-locked views are necessary:
    - Consider using a smaller window near the center of the view and farther away from the person
    - Use a lazy-follow animation

#### Motion in window

- When a window's content moves, the viewer's brain might think that the viewer themself is moving
    - Be mindful about camera motions
        - Keep the content horizon aligned with the real horizon
    - Take note of the focus of expansion: the middle of the screen
    - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10078/Focus_Expansion.jpeg)
        - Move the camera in a way that the motion of the focus of expansion is slow and predictable
        - Keep the focus of expansion within the field of view
            - Avoid fast turns or pure rotational motion. This moves the focus of expansion outside of field of view
    - Keep objects small and at a larger distance for comfort
    -  <img src="/assets/Motion_Consideration_Use_Small_Objects.png"/>
    - Use plain textures and low luminous to reduce motion
    -  <img src="/assets/Motion_Considerations_Use_Plain_Texture.png"/>


#### Oscillating motion

- Avoid oscillations in general, and in particular those with frequencies around 0.2 Hz (1 oscillation every 5 seconds)
- Keep the amplitude of the motion low and make the content semitransparent
- Note It's always a good idea to provide an oscillation-free alternative through the Reduce Motion accessibility setting

#### Key Takeaways For Motion
- Provide a sense of stability
- Avoid head-locked content
- Be gentle with camera motion
- Avoid oscillations
