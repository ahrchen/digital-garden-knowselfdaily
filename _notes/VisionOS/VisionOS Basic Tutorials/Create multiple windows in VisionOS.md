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
</details>

<details>
  <summary><i>Create ColorString  ViewModel to present consistant data</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateColorStringViewModel.png"/>
</details>

<details>
  <summary><i>Create ColorListView to present the ViewModel data</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateColorListView.png"/>
</details>

<details>
  <summary><i>Update MultipleWindowsApp</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/UpdateApp.png"/>
</details> 



<details>
  <summary><i>Create ColorView to present the ViewModel data</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/CreateColorView.png"/>
</details> 

<details>
  <summary><i>Update InfoPList</i></summary>
  <img src="/assets/MultipleWindowsVisionOS/UpdateInfoPList.png"/>
</details> 

<details>
  <summary><i>Run the app!</i></summary>
  <img src="/assets/SwiftUI_WindowGroup/WindowGroup.gif"/>
</details> 

#### For more details see the [video](https://youtu.be/IvMpVgMrSwU)

#### Related Articles
##### WindowGroup [[SwiftUI WindowGroup]]
##### Scene, see Apple tutorial [Specifying the view hierarchy of an app using a scene](https://developer.apple.com/tutorials/swiftui-concepts/specifying-the-view-hierarchy-of-an-app-using-a-scene)
