---
title: Meet Core Location for spatial computing
---

### [Meet Core Location for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10146/)

The next step Apple suggest is to learn about the tools, learn core location for spatial computing.

"Discover how Core Location helps your app find its place in the world — literally. We'll share how you can build a spatial computing app that uses a person's location while respecting their privacy. You'll also learn how your app can request location access and how Core Location adapts requests from compatible iPad and iPhone apps.

" -Apple

#### How to use Core Location
- Discover streamlined location updates
    - We request live updates from CLLocationUpdate, and we'll get them asynchronously down here as they become available.


```swift 
@MainActor class LocationsHandler: ObservableObject {
    private let manager: CLLocationManager
    @Published var lastLocation = CLLocation ()
    private init() {
        self.manager = CLLocationManager() // Safe to call here in MainActor
        self.manager.requestWhenInUseAuthorization()
    }
    func startLocationUpdates () {
        task = Task() {
            do {
                let updates = CLLocationUpdate.liveUpdates ()
                for try await update in updates {
                    if let loc = update.location { /* handle location here */ }
                }
            } catch { /* handle errors */ }
            return
        }
    }
}
```

- Apps must request the user's permission before accessing sensitive information such as location, so here, we invoke this API to do so.
![](https://www.wwdcnotes.com/images/notes/wwdc23/10146/permission.jpg)

- prompt shown to the user requesting this access. So let's see how this looks when we run it in the simulator.
    - Updates only with user consent
    - Invoke requestWhenInUseAuthorization
    - Ask only when needed
![](https://www.wwdcnotes.com/images/notes/wwdc23/10146/request.jpg)

- A user can grant location access for just this session, while using the app, or deny it entirely. Users may also choose to grant your application knowledge of either their precise or approximate location using the highlighted button, just like on iOS.

    - For more information on how exactly this precise versus approximate location works, please refer to [What's new in location from WWDC20](https://developer.apple.com/wwdc20/10660)

    - So what exactly did I mean by "precise location"? You should expect accuracy similar to that of a Mac, so that's about 100 meters.

    - This will be sufficient for applications like those used for finding nearby restaurants, parks, and other attractions.
    
    - However, if your iPhone is nearby, this device can leverage existing connections between these two devices to improve the location accuracy you would get from the headset to be on the same level as that of an iPhone.Your device works even better when together with our other Apple hardware.

- Let us call back to [What's New In Core Location" from WWDC2019](https://developer.apple.com/wwdc19/705) where we discussed how and when foreground apps are considered to be in use on iOS.

-  For a fully immersive experience, as long as the user is running your application, we consider it to be in use and eligible to get location updates, assuming that the user has granted consent for your app to get their location.

- On this system, Core Location provides location information to your app, so long as the user has recently looked at the app. So long as the user is not interacting with or looking at either app, neither one will be able to get location updates. If the user starts looking at -- that is, interacting with -- the app on the left, that app can now get location updates, while the right one still cannot, even if it happens to be in the user's peripheral vision.

![](https://www.wwdcnotes.com/images/notes/wwdc23/10146/looking.jpg)

- And this will remain true until the user looks somewhere else, such as at the app on the right, or moves the two apps together such that they can look at both of the apps at the same time. Just like in iOS, there is also a grace period before Core Location considers the app to no longer be in use.

- This means that if the user were to look at an app on the left, then at the app on the right before looking somewhere else, there will be a short period of time -- a few seconds -- when both apps are still eligible to get location before Core Location considers these apps to be out of use.

- As such, apps will not be able to get location updates while they're not running.

#### How will my app behave when running in compatibility mode?

- So what happens if I just run my iPhone or iPad app with no code changes for a device running xrOS?
    - "While using" derives from eyes As already discussed, the "in-useness" of "while in use" derives from where the user has looked recently.
    - Apps which prompt for Always will have their request redirected to request authorization while in use. You will similarly see that Always is not an option for your application under Settings.
    - Some APIs are unsupported on xrOS If your compatible iPhone or iPad app uses region monitoring or our new CLMonitor, it will not be delivered events. Consider if your iOS app is designed in such a way that assumes a particular API is always supported, and might behave in unexpected ways if, for example, monitoring APIs never deliver events. Similarly, consider whether your app relies on getting location updates in the background while it's not running.


#### To learn more about our API in general, I would recommend that you watch these other two sessions from my colleagues:

- [Discover streamlined location updates - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10180/) discusses some new developments in our API, particularly around how we recommend getting location updates and ways in which we have made our API more compatible with Swift concurrency.

- [Meet Core Location Monitor - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10147/) further discusses new developments in monitoring APIs, and how we've reimagined the ways an app can get notified about events such as geographic entries and exits.
