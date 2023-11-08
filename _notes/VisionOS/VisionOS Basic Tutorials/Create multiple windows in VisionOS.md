---
title: Create multiple windows in VisionOS
---

We will be creating multiple windows in VisionOS using the WindowGroup scene. WindowGroup allows you to present a group of identical structured windows, meaning every window in the group maintain independent state. For more about WindowGroup see [[SwiftUI WindowGroup]]

#### Our final product 
<img src="/assets/SwiftUI_WindowGroup/WindowGroup.gif"/>

#### Step-by-Step
<details>
  <summary><i>Open Xcode and Create a Project</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateNewProject.png"/>
</details>

<details>
  <summary><i>Create ColorString  Model to store data for new windows</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateColorStringModel.png"/>
  
    - line 9 - Import SwiftUI to get access to the struct Color, you will be storing Color into your ColorString object
    - line 11 - Conform the ColorString struct to the Identifiable protocol, you will be needing this to allow an array of ColorString to use id for subscript
    - line 12 - In order to conform to the Identifiable protocol add an id variable of type UUID
    - line 13, 14 - Add string and color vars of String and Color type respectively. We will need those to populate our views with a String and Color. 
    - line 16 - Create an init function to initialize the struct with the respective variables.  
    
</details>

<details>
  <summary><i>Create ColorString  ViewModel to present consistant data</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateColorStringViewModel.png"/>

    - line 11 - Create a static var stub to hard code data for viewModel. It is generally used for previews.
    - line 17 - Populate viewModel with stub data
    - line 19 - Create a custom subscript to retrieve values in the viewModel. 
</details>

<details>
  <summary><i>Create ColorListView to present the ViewModel data</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateColorListView.png"/>
    - line 12 - Get the openWindow from the view environment using the keypath \.openWindow. We will be using this to open up new windows
    - line 16 - Create a ForEach loop to create the desired buttons needed to open new windows
    - line 17 - Set the action of the button to open new window of colorString.id
    - line 19 - Label the button with colorString.string
    - line 22 - Set the background to colorString.color
    - line 23 - Add glass background effect
</details>

<details>
  <summary><i>Update MultipleWindowsApp</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/UpdateApp.png"/>
    - line 12 - Get ColorStringViewModel as source of truth
    - line 16 - Create main WindowGroup to display ColorListView on launching app 
    - line 20 - Create sub WindowGroups to display each colorString in ColorView
    - line 23 - Set the default size of the Window
</details> 

<details>
  <summary><i>Create ColorView to present the ViewModel data</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateColorView.png"/>
    - line 12 - Get ColorStringViewModel as source of truth
    - line 13 - Get Binding variable colorStringId from WindowGroup as source of truth
    - line 16 - If there is a colorStringId, get the colorString and we can create the ColorView
    - line 17 - Instantiate the Text View with colorString.string
    - line 18 - Give the Text View a Frame of 300 by 300
    - line 19 - Give the Frame a background style with the colorString.color
    - line 20 - Enhance the color with glassBackgroundEffect()
</details> 

<details>
  <summary><i>Update InfoPList</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/UpdateInfoPList.png"/>
    - Under Application Scene Manifest, Change the boolean value of Enable Multiple Windows to YES. 
</details> 

<details>
  <summary><i>Run the app!</i></summary>
  <img src="/assets/SwiftUI_WindowGroup/WindowGroup.gif"/>
</details> 

#### For more details see the [video](https://youtu.be/IvMpVgMrSwU)

#### Related Articles
##### WindowGroup [[SwiftUI WindowGroup]]
##### Scene, see Apple tutorial [Specifying the view hierarchy of an app using a scene](https://developer.apple.com/tutorials/swiftui-concepts/specifying-the-view-hierarchy-of-an-app-using-a-scene)
