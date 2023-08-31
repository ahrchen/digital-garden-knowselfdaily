---
title: Create accessible spatial experiences
---

### [Create accessible spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10034/)

This video goes over basic accessibility features, vision, motor, cognitive, and hearing. Designing your application with accessibilitiy in mind helps you design a more accessible application for everybody. 

#### Vision
- Support users who are visually impaired
    - VoiceOver Support
        - Screen reader - Example - HappyBeam 
            - Use Standard Controls
            - Adopt Accessibility Modifiers
            - For more see
                - [Accessibility in SwiftUI](https://developer.apple.com/videos/play/wwdc2019/238)
                - [SwiftUI Accessibility: Beyond the Basics](https://developer.apple.com/videos/play/wwdc2021/10119)
            - Configure accessibility properties on RealityKit Entities
                - Label, value, traits
                - Custom rotors, custom actions, custom content
                    - For More See
                        - [Making Apps More Accessible With Custom Actions](https://developer.apple.com/videos/play/wwdc2019/250)
                        - [VoiceOver efficiency with custom rotors](https://developer.apple.com/videos/play/wwdc2020/10116)
                        - [Tailor the VoiceOver experience in your data-rich apps](https://developer.apple.com/videos/play/wwdc2021/10121)
                - System actions 
            - VoiceOver and Hand input
                - Won't receive hand input by default
                    - Allow for safe exploration for people using VoiceOver
                - Direct Gesture Mode
                    - App receives hand input
                    - VoiceOver does not process its own gestures
                    - Post Announcements that describe the scene, meaningful events, context change
                        - Number of clouds in front
                        - Heart gesture recognized
                        - Cloud state changes
                        - New rooms, environments, or items
                - Choose either normal or VoiceOver state.
                
        - Visual Design 
            - Support Dynamic Type
            - Alternate layouts at largest accessibility text size
            - 4:1 contrast ratio between foreground and background color
            - For More See
                - [Make your app visually accessible](https://developer.apple.com/videos/play/wwdc2020/10020)
            - Use Head Anchors sparingly / Use world anchors
        - Motion
            - Reduce Motion Enabled
                - Rapid Movements
                - Bouncing/wave-like movements
                - Zooming animations
                - Multi-axis movement
                - Spinning/rotation effects
                - Persistent Background effects

#### Motor
- Support users with physical disabilities with eye/hands
    - Go hands-free with Dwell Control
        - Tap, Scroll, Long Press, Drag
    - Pointer Cotnrol
        - Eyes, Head, Wrist, Index Finger
    - Allow people to bypass movement


#### Cognitive
- Support people who learn, remember, and process information differently
    - Guided Access
        - Promotes Focus
            - Restricts people to a single App
        - Minimizes Distractions
            - Background other apps
            - Removes ornamental UI
            - Suppresses hardware buttons
        - For More See
            - [Create accessible Single App Mode experiences](https://developer.apple.com/videos/play/wwdc2022/10152)
    - Best Practice
        - Reduce complex hand gesures -> Hard to learn
        - Create consistent and familiar UI
        - Give people time to enjoy your app

#### Hearing
- Support people with hearing difficulties
    - Add Captions Phases All at once and are easy to read 
    - No roll out Captions
    - AVKit and AVFoundation handle Captions
    - See API
