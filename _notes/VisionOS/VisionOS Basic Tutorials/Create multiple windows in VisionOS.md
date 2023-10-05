---
title: Create multiple windows in VisionOS
---

We will be creating multiple windows in VisionOS using the WindowGroup scene. WindowGroup allows you to present a group of identical structured windows, meaning every window in the group maintain independent state. 
- [ ]  To learn more about WindowGroup see [[SwiftUI WindowGroup]]

Here is the final product that we will be creating
<img src="/assets/SwiftUI_WindowGroup/WindowGroup.gif"/>

#### Step-by-Step
1. Open Xcode and Create a Project 
<img src="/assets/MultipleWindowsVisionOS/CreateNewProject.png"/>

2. Create ColorString  Model to store data for new windows
<img src="/assets/MultipleWindowsVisionOS/CreateColorStringModel.png"/>

3. Create ColorString  ViewModel to present consistant data
<img src="/assets/MultipleWindowsVisionOS/CreateColorStringViewModel.png"/>

4. Create ColorListView to present the ViewModel data
<img src="/assets/MultipleWindowsVisionOS/CreateColorListView.png"/>

5. Update MultipleWindowsApp
<img src="/assets/MultipleWindowsVisionOS/UpdateApp.png"/>

6. Update InfoPList
<img src="/assets/MultipleWindowsVisionOS/UpdateInfoPList.png"/>

7. Create ColorView to present the ViewModel data
<img src="/assets/MultipleWindowsVisionOS/CreateColorView.png"/>

8. Run the app!

#### For more details see the [video](https://youtu.be/IvMpVgMrSwU)

#### Related Articles
##### WindowGroup [[SwiftUI WindowGroup]]
##### Scene, see Apple tutorial [Specifying the view hierarchy of an app using a scene](https://developer.apple.com/tutorials/swiftui-concepts/specifying-the-view-hierarchy-of-an-app-using-a-scene)
