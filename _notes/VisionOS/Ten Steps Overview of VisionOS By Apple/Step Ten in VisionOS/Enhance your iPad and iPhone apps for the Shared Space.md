---
title: Enhance your iPad and iPhone apps for the Shared Space
---

### [Enhance your iPad and iPhone apps for the Shared Space](https://developer.apple.com/videos/play/wwdc2023/10094/)

The next step Apple suggest is to learn about the converting your iPad and iPhones apps for the shared space.

"Get ready to enhance your iPad and iPhone apps for the Shared Space! We'll show you how to optimize your experience to make it feel great on visionOS and explore Designed for iPad app interaction, visual treatments, and media."
-Apple


#### Overview
- Most iPad and iPhone apps run great without any changes, taking advantage of the hard work you've already done and making it work on Apple's latest platform. 
- If you're just getting started, watch [[Run your iPad and iPhone apps in the Shared Space]] first to learn about the system's built-in behaviors, functional differences, and testing setup. 
- In this video, I'll go over how to enhance your iPad or iPhone app from a great app to one that feels at home on this new platform. 
- I'll review the new 
    - interaction, 
    - visual-appearance changes, and 
    - media recording and playback functionality your app should expect. 

#### Interaction
- Interaction on this platform is fun and feels familiar. 
- One of the key components is the new natural input technique. 
    - Tap allows people to look at a button, then tap their fingers together to interact. 
    - People can tap to toggle, tap, hold and swipe to interact with a slider, or tap a button.

    - Direct touch requires reaching out to the app and touching the button in the space with one finger. 
    - Regardless of interaction method, the button provides continuous visual feedback to help with interaction accuracy. 
    - In this video, the cursor represents where a person is looking. When looking at a button, a highlight hover effect tints the control's color to help understand where focus is. 
        - Notice that each item highlights while looking through this list. That highlight follows focus to the left, or right so it's clear what's happening. 
    - Hover effects exist on controls to inform where people are looking. Controls that are inactive do not get hover effects. 
        - System controls take care of all these hover effects for you. If you're only using the standard controls, you're ready to rock and roll without any changes here. 
        - If you're building custom controls, your hover effects may need some tuning. 
- Here's an example of an app with a card-based interface on iPad. Each card contains a photo, title, date, and menu button. 
    - Here is that same app running in Simulator. Because the menu button is a system control, it's already working as expected. 
    - However, each card is a simple VStack with a .onTap modifier, so it does not receive hover effects. 
    - That entire card is a tap target, so it needs hover effects to inform people it has an available interaction. 
    - Let's focus on one of those cards to fix it. System controls, like Button, receive hover effects automatically, so the button used as a menu here already has a hover effect. 
    - However, in this example, people click the entire card to view more detail. By adding .hoverEffect onto the VStack, the entire card becomes available for interaction update and informs people it's tappable. 
```swift
struct TappableCard: View {
   // Sample card
   var imageName = "BearsInWater"
   var headline = "Bear Fishing"
   var timeAgo = "42 Minutes ago"
   
   var body: some View {
      VStack {
         VStack(alignment: .leading) {
            Image(imageName)
               .resizable()
               .clipped()
               .aspectRatio(contentMode: .fill)
               .frame(width: 300, height: 250, alignment: .center)
            Text(headline)
               .padding([.leading])
               .font(.title2)
               .foregroundColor(.black)
         }
         Divider()
         HStack {
            HStack {
               Text(timeAgo)
                  .frame(alignment: .leading)
                  .foregroundColor(.black)
            }
            .padding([.leading])
            Spacer()
            VStack(alignment: .trailing) {
               Button { print("Present menu options") } label: {
                  Image(systemName: "ellipsis")
                     .foregroundColor(.black)
               }
            }
         }
         .padding(EdgeInsets(top: 5, leading: 5, bottom: 5, trailing: 5))
      }
      .frame(width: 300, height: 350, alignment: .top)
      .hoverEffect()
      .background(.white)
      .overlay(
         RoundedRectangle(cornerRadius: 10)
            .stroke(Color(.sRGB, red: 150/255, green: 150/255, blue: 150/255, opacity: 0.1), lineWidth: 3.0)
      )
      .cornerRadius(10)
      .onTapGesture {
         print("Present card detail")
      }
   }
}
```
- Many custom video players have optimized hit targets so people don't have to be quite so precise to interact with them. 
    - In this example of a custom video player on iPad, the tap targets are significantly larger than the symbols on the skip forward and skip backward buttons. 
    - The bordered boxes here show the size of the tap targets where people can interact. On Simulator now, hover effects highlight those tap targets, which shows a tappable region over the entire area. 
    - That same example in the Shared Space now shows the hidden attributes with hover effects. This change of appearance is exposing the truth but does not feel correct.
    - If we zoom into our example, to keep the existing tapping behavior with reduced appearance, add a custom shape to the .contentShape modifiers. 
    - By using a custom shape, apps can provide an origin and size to the .contentShape modifiers, which will be smaller than the tappable region. 
    - In this video, people looking directly at the button will see a hover effect. 
    - And with this change, tapping outside the hover effect bounds will match expectations from iPad and iPhone experiences. Back on the simulator with the full example. 
    - Now with this custom shape, the hover effect appears on just the buttons but allows tapping outside of them. 
    - Excellent! In most cases, hover effects on system controls work great; however, the ability to customize hover effects is powerful. 
```swift
struct ContentView: View {
   var body: some View {
      VStack {
         // Video player
         HStack {
            Button { print("Going back 10 seconds") } label: {
               Image(systemName: "gobackward.10")
                  .padding(.trailing)
                  .contentShape(.hoverEffect, CustomizedRectShape(customRect: CGRect(x: -75, y: -40, width: 100, height: 100)))
                  .foregroundStyle(.white)
                  .frame(width: 500, height: 834, alignment: .trailing)
            }
            Button { print("Play") } label: {
               Image(systemName: "play.fill")
                  .font(.title)
                  .foregroundStyle(.white)
                  .frame(width: 100, height: 100, alignment: .center)
            }
            .padding()
            Button { print("Going into the future 10 seconds") } label: {
               Image(systemName: "goforward.10")
                  .padding(.leading)
                  .contentShape(.hoverEffect, CustomizedRectShape(customRect: CGRect(x: 0, y: -40, width: 100, height: 100)))
                  .foregroundStyle(.white)
                  .frame(width: 500, height: 834, alignment: .leading)
            }
         }
         .frame(
              minWidth: 0,
              maxWidth: .infinity,
              minHeight: 0,
              maxHeight: .infinity,
              alignment: .center
         )
      }
      .frame(
           minWidth: 0,
           maxWidth: .infinity,
           minHeight: 0,
           maxHeight: .infinity,
           alignment: .topLeading
      )
      .background(.black)
   }
}

struct CustomizedRectShape: Shape {
   var customRect: CGRect
   
   func path(in rect: CGRect) -> Path {
      var path = Path()
      
      path.move(to: CGPoint(x: customRect.minX, y: customRect.minY))
      path.addLine(to: CGPoint(x: customRect.maxX, y: customRect.minY))
      path.addLine(to: CGPoint(x: customRect.maxX, y: customRect.maxY))
      path.addLine(to: CGPoint(x: customRect.minX, y: customRect.maxY))
      path.addLine(to: CGPoint(x: customRect.minX, y: customRect.minY))
      
      return path
   }
}
```

- With the new hover effect API, apps can create hover effects for custom buttons, custom shapes, or even opt out of a control if necessary. 
    - Let's inspect how to do that. .buttonStyle is a great way to consistently apply a custom style to all buttons in apps. 
    - When applying custom styling, it turns off hover effects. 
    - To reenable hover effects on a custom .buttonStyle button, add the .hoverEffect() modifier to app elements. 
    - Here is my simple button with a custom button style. Looking at the custom button style, here, we need to add the .hoverEffect modifier to add hover effects to the button with custom styling. 
    ```swift
    struct ContentView: View {
        var body: some View {
            VStack {
             Button("Howdy y'all") { print("🤠") }
                .buttonStyle(SixColorButton())
            }
            .padding()
        }
    }

    struct SixColorButton: ButtonStyle {
       func makeBody(configuration: Configuration) -> some View {
          configuration.label
             .padding()
             .font(.title)
             .foregroundStyle(.white)
             .bold()
             .background {
                // Background color bands
                ZStack {
                   Color.black
                   HStack(spacing: 0) {
                      // GREEN
                      Rectangle()
                         .foregroundStyle(Color(red: 125/255, green: 186/255, blue: 66/255))
                         .frame(width: 16)
                      // YELLOW
                      Rectangle()
                         .foregroundStyle(Color(red: 240/255, green: 187/255, blue: 64/255))
                         .frame(width: 16)
                      // ORANGE
                      Rectangle()
                         .foregroundStyle(Color(red: 225/255, green: 137/255, blue: 50/255))
                         .frame(width: 16)
                      // RED
                      Rectangle()
                         .foregroundStyle(Color(red: 200/255, green: 73/255, blue: 65/255))
                         .frame(width: 16)
                      // PURPLE
                      Rectangle()
                         .foregroundStyle(Color(red: 134/255, green: 64/255, blue: 151/255))
                         .frame(width: 16)
                      // BLUE
                      Rectangle()
                         .foregroundStyle(Color(red: 75/255, green: 154/255, blue: 218/255))
                         .frame(width: 16, height: 500)
                   }
                   .opacity(0.7)
                   .rotationEffect(.degrees(35))
                }
             }
             .cornerRadius(10)
             .hoverEffect()
       }
    }
    ```
- Many apps have fun and custom interfaces. In this example of a beekeeping app, buttons are honeycombs, where each honeycomb cell is its own tap target. 
    - Apps implementing custom shape buttons will need to inform the system how to render their hover effects. 
    - Frame width here is larger than the area the shape occupies, so the default system-provided hover effect covers the entire button frame, unbounded to shape. 
    - By passing a custom shape to the .contentShape modifier, hover effects will trim to the button's bounds. Let's add that here. Now it is perfect, because when people look at individual buttons, the hover effect is trimmed to the geometry of the button's shape. 
    ```swift 

    struct ContentView: View {
        var body: some View {
          VStack {
             Button { print("🐝") } label: {
                // Button label
                HoneyComb()
                   .fill(.yellow)
                   .frame(width: 300, height: 300)
                   .contentShape(.hoverEffect, HoneyComb())
                }
             }
             .frame(width: 400, height: 400, alignment: .center)
             .background(.black)
             .padding()
          }
        }
    }

    struct HoneyComb: Shape {
       func path(in rect: CGRect) -> Path {
          var path = Path()
          path.move(to: CGPoint(x: rect.minX + (rect.width * 0.25), y: rect.minY))
          path.addLine(to: CGPoint(x: rect.maxX - (rect.maxX * 0.25), y: rect.minY))
          path.addLine(to: CGPoint(x: rect.maxX, y: rect.midY))
          path.addLine(to: CGPoint(x: rect.maxX - (rect.maxX * 0.25), y: rect.maxY))
          path.addLine(to: CGPoint(x: rect.minX + (rect.width * 0.25), y: rect.maxY))
          path.addLine(to: CGPoint(x: rect.minX, y: rect.midY))
          path.addLine(to: CGPoint(x: rect.minX + (rect.width * 0.25), y: rect.minY))
          return path
       }
    }
    ```
##### Opt Out
- System controls that are disabled due to app state automatically do not get hover effects.
-  If apps want to de-emphasize specific interface elements, they can opt out individual items. 
-  People expect hover effects to be apparent and consistent across the system, so they should be turned off sparingly. 
-  The system accepts a maximum of two simultaneous inputs since each hand is a distinct touch. 
    -  Custom gesture recognizers are also supported, but you may need to update them to run smoothly with the natural input expectations. 

##### Game Controller Support
-  Games, or other apps that need rapid or simultaneous input, need to support game controllers. 
-  iPad and iPhone apps have long been able to indicate support for game controllers. 
-  On this platform, it's even more critical for additional input methods. By including GCSupports ControllerUserInteraction in the Info.plist and adding Game controller capability, it adds a badge to the app's product page. 
-  This improves communication with people using App Store to find games, and makes the availability of game controllers even more evident across all platforms. 
-  For information about game controllers and games on App Store, watch the videos 
    -  [Advancements in Game Controllers](https://developer.apple.com/videos/play/wwdc2020/10614)
    -   [[Build great games for spatial computing]] 

#### Visuals
-   iPad and iPhone apps running on this platform match their iPad light-mode appearance. In most cases, that looks great. 
-   If you're using system standard controls, layouts, and colors, there's no new work for you here. 
-   The system optimizes rendering, using dynamic content scaling so all images and text are always sharp at any angle, from any distance. 
    -   To provide the best experience, use vector-based content. Prompts on iPad and iPhone are presented modally, so the prompt must be interacted with before continuing. 
-   On this new platform, prompts do not present modally. 
    -   Prompts such as asking for location permission, Sign in with Apple, or OAuth, do not require handling before continuing. 
    -   These interfaces create their own chrome and windowed experience. Apps should be aware and handle cases where they get the prompt, but may not get immediate cancelled or success call backs. 

#### Media
-   People capturing, sharing, and posting content is a great way to express themselves. On this platform, there are some differences apps should be aware of. 
-   There are multiple external and internal facing cameras. However, many of these cameras are not available for app use. 
    -   It is critical to use discovery sessions to detect which cameras and microphones are available for use. 
    -   To ensure apps have an excellent capture experience, use AVCaptureDevice.DiscoverySession to confirm hardware availability. 
    -   Additionally, similar to other platforms, requesting permission before use is required. 
-   Lastly, generalize your authorization prompt string to inform people of use, without mentioning specific hardware or software versions.

- When apps request camera and microphone availability, expect different values to be returned than iPad and iPhone. 
    - When querying microphone, apps will receive a single .front location microphone. 
    - When querying camera, apps will find two cameras. 
    - The .back camera returns a black camera frame with a no camera glyph. 
    - This is a nonfunctional camera to support apps that assume back camera availability. 
    - When querying for front camera, apps find a single composite camera. 
    - If no spatial persona is found on a device, then no camera frames will return to apps. 
##### Media playback
- AVRoutePickerView and Picture in Picture are unavailable on this platform, which has been reflected in system-provided players. 
- Apps that implement custom players need to check both availabilities before showing these controls. 
- Lastly, this platform locks once removed. Apps that utilize background audio should consider this difference, as they will no longer get this background mode when the device is locked, and will be fully suspended. 
    - Apps that import media should consider alternative sources when capture hardware isn't available. 
    - Options such as iCloud or content pickers, like document or photo picker, are excellent alternatives. 
    - Additionally, apps that use VisionKit's VNDocumentCameraViewController will automatically capture with Continuity Camera on a nearby device. 
    - These alternatives bring even more media-import options to existing iPad and iPhone apps. iPad and iPhone apps run great on this new platform. 
#### Conclusion
- Make sure hover effects are added to all your interactive controls. 
- For games, add controller support to ensure players continue to have a great experience. 
- Finally, review your assumptions about camera and microphone presence by checking for availability before use. 
