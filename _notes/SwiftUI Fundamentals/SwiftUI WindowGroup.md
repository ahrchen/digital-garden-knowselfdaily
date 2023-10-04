---
title: SwiftUI WindowGroup
---

### What is WindowGroup?

WindowGroup is one of six default scene type available to you in 2023. The scene types include, WindowGroup, DocumentGroup, Settings, Window, MenuBarExtra, Immersive Space. Speaking of Scene, Scene acts as a container for a view heirarchy that you want to display to users. 

For example
<details>
  <summary><i> MenuBarExtra, places items in your Mac tool bar.</i></summary>
  <img src="/assets/SwiftUI_WindowGroup/MenuBarExtra.gif"/>
</details>

<details>
  <summary><i> Settings, provides a settings view heirarchy.</i></summary>
  <img src="/assets/SwiftUI_WindowGroup/Settings.gif"/>
</details>

<details>
  <summary><i> Window Provides a single screen.</i></summary>
  <img src="/assets/SwiftUI_WindowGroup/Window.gif"/>
</details>

WindowGroup in particular allows you to present a group of identical structured windows, meaning every window in the group maintain independent state.
<img src="/assets/SwiftUI_WindowGroup/WindowGroup.gif"/>

#### For more details on WindowGroup, see tutorial [[Create multiple windows in VisionOS]]
#### For more details on Scene, see Apple tutorial [Specifying the view hierarchy of an app using a scene](https://developer.apple.com/tutorials/swiftui-concepts/specifying-the-view-hierarchy-of-an-app-using-a-scene)
