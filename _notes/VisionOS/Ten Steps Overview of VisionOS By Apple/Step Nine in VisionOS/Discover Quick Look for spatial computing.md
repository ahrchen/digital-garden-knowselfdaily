---
title: Discover Quick Look for spatial computing
---

### [Discover Quick Look for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10085/)

The next step Apple suggest is to learn about the Quick Look on VisionOS, lets check out how Quick Look adds powerful previews for 3D content.

"Learn how to use Quick Look on visionOS to add powerful previews for 3D content, spatial images and videos, and much more. We'll show you the different ways that the system presents these experiences, demonstrate how someone can drag and drop Quick Look content from an app or website to create a separate window with that content, and explore how you can present Quick Look directly within an app."
-Apple

#### Overview

- Quick Look is a system framework that allows you to easily preview and edit files on iOS, macOS, and now xrOS. 
- Quick Look comes with powerful editing features like trimming for videos and Markup for PDFs and images right out of the box. 
- It also handles the secure and safe access of files, so you don't have to worry about opening up untrusted files in your app. 
- Quick Look shows up in many places across Apple's platforms. 
    - On iOS, you see it whenever you open an attachment from a message thread. 
    - On macOS, you enter Quick Look whenever you hit the Space bar on a selected file from Finder or desktop. 
    - Quick Look is the system viewer for file-backed content on xrOS. And just like on iOS and macOS, xrOS apps can leverage Quick Look to easily gain feature-rich file viewing and editing. 
        - Let's see what that looks like. Recently, I've been working on remodeling an apartment, and I've been using an app to track the progress of that project and collaborate with my team. 
        - One of the interior designers I'm working with just sent me a folder with some ideas he has for the house. I have that folder opened up here so let's see what he came up with. 
        - It looks like there's a USDZ model of the proposed living room. Let's open it up. To do this, I'll pinch and drag the file out and drop it outside of any application.
        - Dropping the USDZ file presents a 3D Quick Look preview right where I dropped it. And I can immediately start to interact with it. Using a pinch and drag gesture, I can rotate the model to get a better look at the beautiful exposed brick facade. 
        - To take a closer look at the living room, I'll just zoom into the model to scale it up. 
        - It looks like my designer also sent a picture of the neighborhood surrounding the home.
        -  Finally, it looks like there's a document here with a list of the features planned for the home. A lot of these look great but I'm not sure about this last one, so let me leave a note to get back to it later. I'll open up the menu at the top of the window and select Markup, which brings up the Markup palette. Let me quickly circle the item I want to get back to.

    - We were able to drag a file from an application and preview it outside of that app. We did this with multiple files and viewed them all alongside the source application. 
- This new way to present files in Quick Look is called Windowed Quick Look. 
- In this session, we'll learn more about this presentation style and how apps and websites can adopt it. 
- Then we'll go over how to present Quick Look previews directly within an application. 
- 
#### Windowed Quick Look
- But first, let's take a deeper dive into Windowed Quick Look. 
    - Windowed Quick Look allows you to present Quick Look previews outside of your application. This is perfect for nonblocking experiences where you want to be able to view your file content alongside your app. 
    - Since windowed Quick Look previews are hosted in a separate app, you can close your application while still having those previews persist. 
    - Windowed Quick Look also offers a much richer viewing experience for 3D models backed by USDZ and Reality files. 
        - You can scale and place 3D content independent of your application. 
        - You can also scale the 3D model which will dim the environment and hide all other scenes, allowing you to focus on just the 3D content. 
        - Certain file types presented in Quick Look windows offer SharePlay experiences so you can share a file and view it over FaceTime. 
        - When sharing 3D content over SharePlay, Quick Look will sync the 3D model's orientation, scale, and animations. 
        - When sharing images over SharePlay, you'll be able to mark up that image together with others. 
        - SharePlaying files with Quick Look offers you an easy and simple way to collaborate on files with a group. 
    - Both applications and websites can present content in Quick Look windows and take advantage of the many benefits it has to offer. 
        - First, let's take a look at how apps can present Windowed Quick Look. 
            - Apps can present files in Quick Look windows by providing a drag source containing some URL. 
            - During a drag-and-drop interaction, when a drop target is outside of any app, the system will copy and present your provided URL in a Quick Look window. 
            - If your provided URL is pointing to a file hosted in a remote destination, like iCloud, the system will download it first. 
                - Keep in mind, that because a copy of your provided file is presented, any edits such as markups on an image made to the presented file will not be written back to the URL you provide. To see this in action, let's go to Xcode.

##### Xcode example
###### In-App
- Before we add drag support to our app, let me quickly give you an overview of the app. The app lets you see the progress of the project and view a list of the files shared by other team members. 
    - Here we have a list view which displays FileViews. Since we want to be able to drag out each file, we'll need to turn each FileView into a drag source. 
    - To do this, I'll add the onDrag modifier onto the FileView. The onDrag modifier expects an NSItemProvider, so I'll return an item provider containing the URL for the file being displayed in that FileView.
    ```swift
    import Foundation
    import SwiftUI
    import UniformTypeIdentifiers

    struct FileList: View {

        @State var files: [File]
        @State var previewedURL: URL? = nil
        @State var selectedFile: File? {
            didSet {
                self.previewedURL = selectedFile?.url
            }
        }

        var body: some View {
            List(files, selection: $selectedFile) { file in
                Button(file.name) {
                    selectedFile = file
                }
                .onDrag {
                    return NSItemProvider(contentsOf: file.url) ?? NSItemProvider()
                }
            }
        }
    }
    ```
    - Building and running the app in the simulator, I can now drag out from the file view and present that file in a new Quick Look window. 
    - I can also close out my app and still have that file's preview displayed. By adding just a few lines of code, I've enabled drag and drop within my app and allowed content to be viewed in a separate window letting me still use my app freely. 
###### Website
- Now let's see how we can do this for websites. 
- Since iOS 12, websites have been able to link to and view 3D content in AR Quick Look on iPhone and iPad by marking up links with the AR attribute. 
- When you open a link to marked-up 3D content on xrOS, Safari will present the 3D content in a new Quick Look window. 
    - Websites already supporting AR content linking on iOS and iPadOS will have this behavior carry over to xrOS with no additional work needed. 
    - xrOS will also respect customization options such as disabling content scaling. 
    - For more information on those customization options, see the [Advances in AR Quick Look](https://developer.apple.com/videos/play/wwdc2019/612/) session from WWDC19. 
    - If you haven't setup your website to present 3D content from Safari, all you have to do is mark up your links like this. 
        - By adding rel="ar" to your link or anchor element, Safari won't navigate on tap. 
        - Instead, it will present that 3D file in a Quick Look window alongside the website. 
        - Let's go over to Safari and check this out. We have the AR Quick Look gallery page open in Safari here. There are a bunch of 3D models linked to from this page so let's open some of them up. 
        - Tapping on a link to this teapot, downloads and presents that 3D model in a Quick Look window. Once it downloads, the model will appear. 
        - Tapping on the link to this mug presents it near the teapot and Safari. This is really great for e-commerce sites where you might want to view and place products in shared space to get a sense if it's right for you. 
        - We just went over presenting files in a Quick Look window to preview it outside your app. There are some use cases where you may want to preview files directly inside of your app. 
        - 
#### In-app Quick Look 
- Displaying in-app Quick Look content is as simple as passing in some URLs to the quickLookPreview function in SwiftUI. 
        - When presented using quickLookPreview, the preview will display as a sheet on top of your view's content. If you want more customization options over your presented previews, you can use a QLPreviewController here instead. 
        - If you're bringing your iOS app to xrOS, existing uses of quickLookPreview or QLPreviewController API will carry over for free. 
- Let's hop over to the simulator and see where we could take advantage of this in our Project Tracker app. I have a view where I can review some new designs my team has before sending them off to the homeowner for approval. I can currently see a list of files, but I can't actually preview any of the files. Let's go to Xcode and see if we can fix this. This is my view right now. 
    - To preview the files directly in my application, 
    - first I'll import QuickLook. 
    - Then I'll add the SwiftUI quickLookPreview function passing all of the files I want to preview and the specific file I want initially selected.

```swift
import Foundation import SwiftUI
struct FileList: View {
  
@State var files: [File]
@State var previewedURL: URL? = nil
@State var selectedFile: File? {
    didSet {
        self.previewedURL = selectedFile?.url
        }
  }
  
var body: some View {
    List(files, selection: $selectedFile) { file in
            Button(file.name) {
                selectedFile = file
            }
        }
        .quickLookPreview($previewedURL, in: files.map { $0.url })
      }
}
```

- Let's run this and see what we get.

- Going back to our app, now when I select this view, I can see a sheet with our previews appear directly within our app. I can cycle through the files using the navigation controls in the toolbar and make sure everything is fine before sending them over to the homeowner. 
- Presenting file previews directly within our app was as easy as passing in some URLs to the quickLookPreview function. Now that we've covered both flavors of Quick Look on the platform, let's touch on the file types with supported previews. 
    - Quick Look supports the most common file types including images, videos, PDFs, and USDZ files. 
    - Spatial images and videos shown in Quick Look will look just as stunning as they do in Photos. 
