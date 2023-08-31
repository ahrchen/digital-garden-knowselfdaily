---
title: Meet Reality Composer Pro
---

### [Meet Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10083)

The next step Apple suggest is to learn about the working with USD(Universal Scene Description) files using Reality Composer Pro.

"Discover how to easily compose, edit, and preview 3D content with Reality Composer Pro. Follow along as we explore this developer tool by setting up a new project, composing scenes, adding particle emitters and audio, and even previewing content on device. Once you're familiar with the basics of Reality Composer Pro, check out "Explore Materials in Reality Composer Pro" and "Work with Reality Composer Pro content in Xcode" to learn more advanced techniques and tips."

-Apple

#### Project setup
- Setup project using the visionOS template
    - Identify the USD file
        - For more about Universal Scene Description 
            - [Understand USD fundamentals](https://developer.apple.com/videos/play/wwdc2022/10129)
            - [Create 3D workflows with USD](https://developer.apple.com/videos/play/wwdc2021/10077)

#### UI navigation
- Moving around view port
    - WASD keys and arrow keys to move around 
    - PS5 Controller for more control
- Heirarchy Panel
    - Search, Organize and Group Assets together
- Inspector Panel
    - Edit properties of objects
    - Add Components
- Editor Panel
    - Project Browser
        - See files
    - Shader Graph
    - Audio Mixer
    - Statistics



#### Composing scenes

- Add assests into project
    1. Import assest that already exist on computer
    2. Content libary
    3. Object capture [Meet Object Capture for iOS](https://developer.apple.com/videos/play/wwdc2023/10191)
- Produce the scene
    - Delete the Sphere 
    - Add Diorama_Base and Yosemite
    - From Content library import SmoothConcrete material
    - Place location pins 
        - El_Capitan 
        - Cathedral_Rocks
        - Merced River
    - Group the location pins for organization

#### Particle emitters
- Two parts
    - Particle
        - Color
        - Properties
        - Force Fields
        - Rendering
    - Emitter
        - Timing
        - Shape
        - Spawning
- Add some clouds
    - Combine to create cloud chunks 
        - Create Cloud_Chunk Scene
            - Add Particle Emitter using Add Component
                - Particles control the appearance of individual particle
                - Emitter control how the particle emits from the set location
            - Set Emitter first
                - Set Idle Duration to 0, no more delay of emission of particles
                - Set the emitter shape from cylinder to sphere to match clouds 
                - Set birth location from surface to volume to match clouds
                - Adjust x and z  to be greater than y scale for width and less height to match clouds
                - Is local space 
                    - All changes to scene will change the particle emitter
            - Set Particle 
                - Birth Rate, the number of particles at a time
                    - Set from 2000 to 500
                - Textures are good
                - Properties
                    - Increase the lifespan from 2 seconds to 5 seconds
    
        - Create a new Scene Cloud_A, Cloud_B, and Cloud_C
            - Import 3 Cloud_Chucks into heirarchy panel
            - Hit the play button to see emission
            - Shift Cloud_Chucks to fill space in differing positions to create variations 
    - Group Cloud_A, Cloud_B, and Cloud_C
        - Click group clouds and click play on inspector panel 


#### Audio authoring
- Audio File
    - Place on Object
    - Object can play one or more Audio File
        - Random Audio File from group is 
        
- Three types of Audio Sources
    - Spatial
        - Position and direction
    - Ambient
        - Direction
            - Wind sounds from the east no matter the position of character
    - Channel
        - No Position nor direction
            - Background music
- Create Build_With_Audio Scene
    - Add bird and two bird call audio file to heirarchy panel
    - At the bottom of the heirarchy panel add Spatial Audio Source
    - At the bottom of the inspector panel add Spatial Audio Source
    - Place Spatial Audio Source at the beak of bird
        - Preview the sound from the bird at the top of the inspector panel
    - Create a audio file group using the plus button at the bottom of the inspector panel
        - Create the audio group bird_calls
- Create 5 birds with audio in Root Scene
- More works needs to be done in Xcode see [Work with Reality Composer Pro content in Xcode](https://developer.apple.com/videos/play/wwdc2023/10273)


#### Statistics
- Click the Statistics tab in the editor panel 
- The collection of catagory
    - General
    - Physics
    - Animation
    - Particle Emitters
    - Audio
    - Materials
    - Geometry
        - 464107 triangles used for the diorama_base, this is too much compared to our terrian
        - import a similar diorama base with fewer triangles
            - down to 2560 trianges
            - keep the same look
    - Textures



#### On-device preview
- preview scene on device
    - click the goggle button on the tool bar
    - see it 

#### Up next
- Add catalina and yosemite in [Explore materials in Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10202)
- Add interactivity in [Work with Reality Composer Pro content in Xcode](https://developer.apple.com/videos/play/wwdc2023/10273)
