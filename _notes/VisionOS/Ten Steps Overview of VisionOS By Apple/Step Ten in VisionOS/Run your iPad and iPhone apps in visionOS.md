---
title: Run your iPad and iPhone apps in visionOS
---

### [Run your iPad and iPhone apps in visionOS](https://developer.apple.com/videos/play/wwdc2023/10274/)

The next step Apple suggest is to learn about the converting your iPad and iPhones apps for the shared space.

"Discover how you can run your existing iPad and iPhone apps on Vision Pro. Learn how iPadOS and iOS apps operate on this platform, find out about the Designed for iPad experience, and explore the paths available for enhancing your app experience on visionOS."
-Apple






#### Overview
- You already have a great app built for them, maybe you even have multiple. Now you can easily run those same apps on Apple's latest platform. 
    - The majority of iOS apps look and feel great right out of the box. 
    - For example, check out the iPad Calendar app running unmodified in the simulator. It looks and feels just like iPad and everything works exactly as I would expect. I can see different timelines, zoom into details about specific events, and add new ones.
    - And Maps, which runs in its iPad version following the recommendations I'm about to cover. I can spin the globe beautifully. I can also look up specific destinations...and visit famous landmarks.

- In this video, I'll introduce iPad and iPhone apps on this new platform. 
    - I'll start by covering the built-in behaviors your app gets for free.

    - Next, I'll talk about the functional differences your app should be aware of and what you should do about them. 

    - Finally, I'll explain how to decide whether the Designed for iPad experience is best suited to your app's needs.

#### Built-in behaviors
- This new platform is built on the foundations of iOS. We enhance that shared bedrock with additional system support. 
- The combination of the two makes it more than likely that your app will run beautifully without changing anything! 
##### Layout
- iPad and iPhone apps are displayed as windows on this device, in their light mode style. 
- The system prefers the iPad variant of your app in landscape orientation, but if your app only supports iPhone, the system displays it with an iPhone aspect ratio in portrait orientation. 
- If your app supports multiple orientations, a rotation button is provided above the top-right corner of your window, so people can rotate each scene to their preference. 
- When you grab the corners of your app, the system scales its window, preserving the aspect ratio. When you reach the minimum or maximum size, the corners bounce to reflect that. 
- The scaling is managed by the system so your app gets all of this support for free. 
##### Input and Interaction
- People interact with content on this device via natural input. They look at something and tap their fingers together to select it or reach out and touch content directly. 
- They may also use a Bluetooth trackpad or game controller. 
- All of these system-defined interaction methods send events that your app is already familiar with so you can continue to leverage the same event-handling techniques that you already use. 
- System views like the document manager and photo picker match the system appearance to help your app fit into the look and feel of the platform. 
- If your app supports Touch ID or Face ID, LocalAuthentication automatically forwards those implementations through Optic ID so your app supports the latest authentication technology without any additional work on your part. 
- Now, there are a few things that are different about this platform compared to iOS. 
##### Orientations & plist
- Apps on this device can be viewed in portrait or landscape. That's nothing new compared to iPad. But unlike iPad, there's no notion of rotating the entire device. 
    - Because the device's orientation doesn't inform your app's orientation, you may want to specify which orientation your app prefers for new scenes. 
    - People can still rotate scenes later via the system rotation button. You can express a preference by adding the new UIPreferredDefaultInterface Orientation key to your app's Info.plist. 
    - If you don't provide one, the system will use its default orientation. 
    - This key is unique to this platform and will not affect other platforms. 
- There are a couple other plist keys that also have special meaning on this device, even though they're not new. 
    - The system uses UISupportedInterfaceOrientations to decide if your app's windows need a rotation button, and 
    - App Store Connect relies on UIRequiredDeviceCapabilities to determine if your app is compatible with this new device.
    -  All suitable apps are automatically made available on the App Store. If your app relies on specific features which are not available on this device or if there's a reason your app doesn't make sense on this platform, you can manage availability in App Store Connect. 
    -  For more information, watch [[Explore App Store Connect for spatial computing]]
    -   Take a moment to add those keys to your Info.plist if necessary or confirm the existing values are still accurate and up to date. 

#### Functional Differences
- Gestures on this device work differently since folks use their eyes and hands to interact with content. 
    - There are a maximum of two simultaneous inputs as each hand is a distinct touch. All system gestures that expect two touches or fewer work seamlessly. 
    - Custom gesture recognizers are also supported, but you may need to update them to run smoothly with the natural input expectations. 
    - One of the most updated frameworks is ARKit which has evolved significantly to be more powerful than ever. 
        - We've designed new APIs and experiences from the ground up to account for fundamental differences in platform architecture and privacy needs. 
        - That means your existing ARViews and ARSessions won't work on this device as they do on iPad and iPhone. 
        - Check out the [Re-imagine your ARKit app for spatial experiences](https://developer.apple.com/videos/play/wwdc2023/10091/) video to learn about all the new ARKit capabilities you can leverage by rebuilding your app for this platform. 
    - Location support for this device is a lot like iPad: location can be approximated via Wi-Fi or shared via iPhone. 
        - More details are provided in the [Meet Core Location for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10146) video. 
    - Look to Dictate is a convenient new input technique that allows people to quickly navigate through an app using only their eyes and voice. When enabled, a microphone icon replaces the magnifying glass in search fields, and you can look at the microphone and speak to search.

        - This API is offered on search bars. It's disabled by default for iPad and iPhone apps running on this platform to allow you to verify the behavior and decide where you want to enable it. And it's a no-op on iOS and iPadOS, so there's no need to conditionalize your support by platform. 
        - You can enable Look to Dictate in SwiftUI by adding the .searchDictationBehavior() modifier to your searchable view. 
        - For UIKit search bars, set isLookToDictateEnabled to true. 
- The best way to handle all of these changes is the same way you always have: use availability checks. 
- Make sure that a framework is supported before calling into it. Many frameworks even have those functions built in for your convenience. 
- Don't forget to do the same thing when accessing configurations that rely on the presence of specific hardware. 
    - For example, the headset has many more cameras than just the front and back cameras on iOS devices, but not all of those are available for apps to use. 
    - Verify that a camera is present and supported before you use it. These practices make your app more robust on every device, not just this one. 
    - That's only a sampling of the framework evolution on this platform. Some frameworks have grown a lot and have videos specifically dedicated to this device, like SwiftUI, ARKit, and RealityKit. 
    - Most of the remaining frameworks work as they always have with a few tweaks to how you adopt them. 
    - Detailed information about all of the modified frameworks is available in the developer documentation. 

 
#### Choose your experience
- Now that you have a sense of what code changes are necessary for your app, you're ready for action. When the xrOS SDK is installed, Xcode automatically adds xrOS Device (Designed for iPad) to the Supported Destinations for projects that use the iOS SDK. 
- If your scheme sets a different platform or auto for the SDK, you can add the Designed for iPad target manually. Once that's set up, a run destination with the matching name will appear in the destination picker. 
- Select that target, build, and run. That's all there is to it! iPad and iPhone apps provide a fantastic experience on this device. 
- Most apps don't need any changes at all, thanks to extensive system support. Whether you want to stick with building your app against the iOS SDK or rebuild against the xrOS SDK depends on your goals. 
- Like I discussed earlier, there are differences in which frameworks are available for each SDK, as well as differences in supported features within each framework. 
    - There are two big things I want to call out that are only available in the iOS SDK: SpriteKit and storyboards. If either of these technologies is integral to your app, you need to stick with designing for iPad. iPad and iPhone apps are displayed in windows that feel just like iPad in their light mode style. 
    - Here's what Maps looks like when zoomed into the Sydney Opera House. Notice how the content fills all the way to the edges of the window but doesn't extend past it, and all of the colors match the same light mode style that Maps uses on iPad and iPhone. 
    - Apps designed for xrOS unlock another level of immersive, spatial experiences. Several frameworks, like ARKit and RealityKit, have evolved functionality that's only available in apps designed for this platform. 
        - Refer to the other videos or the documentation to learn about all the new experiences that are possible thanks to these updates. 
        - In addition to windows, apps designed for this device also support volumes to display 3D objects in containers that grow to fit their contents, as well as Immersive Spaces for immersive experiences. 
        - Here's what the Keynote rehearsal space looks like in headset. By hiding passthrough and other apps, Keynote keeps you fully immersed and focused on your presentation. 
        - In both the headset and the simulator, apps designed for this platform use the system look and feel. 
        - Their backgrounds are a glass material that grounds people in their surroundings and dynamically adjusts color balance and contrast to promote legibility. 
        - They can also take advantage of the new Ornament API. Like the tab bar on the left and buttons at the bottom of Photos, ornaments anchor to the sides of a window to enhance its functionality. 
        - And they leave the app more room to draw within the window. Most frequently, ornaments are used for navigation or toolbars. 
- Designing for xrOS is perfect for apps that want to create immersive experiences, adopt new framework functionality, or match the system look and feel. 
- If you would rather preserve your app's existing experience, designing for iPad is the road for you. 
- This platform shares a common foundation with iOS and iPadOS, so no matter which SDK you choose, the work you do for those platforms will continue to benefit your experience on this one. 

- If you decide that designing for this new platform is the best fit for your app, the 
    - [[Meet SwiftUI for spatial computing]] 
    -  [[Meet UIKit for spatial computing]] 


#### Conclusion    
-  Your next step is to try your app on this exciting new platform! The vast majority of apps work without any code changes at all. Pay special attention to the compatibility areas I covered: ensure your Info.plist keys are up to date, opt into new platform experiences you're interested in, and verify that your framework dependencies are available before you use them. Once you've done all that, watch [[Enhance your iPad and iPhone apps for the Shared Space]]
