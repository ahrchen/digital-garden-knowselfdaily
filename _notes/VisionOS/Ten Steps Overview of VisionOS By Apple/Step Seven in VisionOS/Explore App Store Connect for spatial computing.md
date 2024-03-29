---
title: Explore App Store Connect for spatial computing
---

### [Explore App Store Connect for spatial computing](https://developer.apple.com/videos/play/wwdc2023/10012/)

The next step Apple suggest is to learn about the App Store Connect and TestFlight. We need to deploy our app and collect feedback to improve.

"App Store Connect provides the tools you need to test, submit, and manage your visionOS apps on the App Store. Explore basics and best practices for deploying your first spatial computing app, adding support for visionOS to an existing app, and managing compatibility. We'll also show you how TestFlight for visionOS can help you test your apps and collect valuable feedback as you iterate."
-Apple


#### Set up your app
##### In App Store Connect, you have three options to choose from when setting up your app.

- You can create a new app with the xrOS platform.
    - This is the option to select if you're introducing a new app to the App Store for the first time, or if you want to configure your xrOS app to have a different price or availability than your other apps.

 - You can also add the xrOS platform to an existing app to create a universal purchase.

    - This allows your users to enjoy your app and in-app purchases across all platforms.

    - Your app will have the same name and URL across all platforms, making it easier for users to find it.

    - Your app will automatically install for users across their devices when they have automatic downloads enabled.

- And finally, you can choose to make your compatible iPad and iPhone apps available on xrOS without making any code changes or submitting a new build.

    - This is a great option if you're still working on your xrOS app, but you want users on xrOS devices to enjoy your app as soon as possible.

##### Examples of the three options
- OK, let's look at each of these options in App Store Connect, starting with creating a new app.

    - Let's say I'm a developer on the Nature Lab team, and I'm excited to create a fully immersive app for my customers.

    - I'm planning to introduce Backyard Birds to the App Store.

    - Since Backyard Birds is a new app, I'll first need to create a new app record.

    - I can do this by clicking the plus (+) button in the upper-left area of the Apps page, and then selecting New App from the drop-down menu.

    - From the New App dialog, I'll select xrOS under Platforms, and then fill in the remaining fields like Name, Bundle ID, and SKU.

    - That's it! I'll just need to click Create to complete the new app record for Backyard Birds, then I can begin uploading builds.

- Next, let's look at adding xrOS to an existing app.

    - I'm back on the Apps page for my Nature Lab team.

    - My customers love tracking their favorite mountain climbing routes with Mountain Climber on iOS, so I decided to introduce a new experience on xrOS.

    - To add the xrOS platform, I'll select my Mountain Climber app.

    - And from here, I'll click Add Platform from the left sidebar.

    - On the Add Platform dialog, I'll just need to select xrOS, then click Add.

    - Once the platform is added, I can then begin uploading builds for Mountain Climber.

    - And finally, all compatible iPad and iPhone apps are automatically made available on the App Store on xrOS.

- If there's any reason why you think your app doesn't make sense on the platform, you can manage its availability on xrOS.

    - Let's take a look.

    - On the Apps page, click the ellipsis (…) button in the upper-left area, then select "iOS Apps on xrOS Availability" from the drop-down menu.

    - From here, you have full control over managing which apps are made available on xrOS.

    - If your compatible iPad and iPhone app is made available by using this option and you later add the xrOS platform, releasing it will replace the iOS app version on the App Store.

    - For the Nature Lab team, I wanted to make sure that all of our compatible apps are made available, so I'll keep the default settings here.

    - You can also manage an individual app's availability from the Pricing and Availability page.

    - Under the iPhone and iPad Apps on xrOS section, you have the option to “Make this app available”.

    - You can also verify if your current and upcoming app versions are compatible with xrOS.

- To learn more about compatible iPad and iPhone apps and how to make sure your apps run properly, check out the sessions 
    - ["Run your iPad and iPhone apps in the Shared Space"](https://developer.apple.com/videos/play/wwdc2023/10090) 
    -  ["Enhance your iPad and iPhone apps for the Shared Space"](https://developer.apple.com/videos/play/wwdc2023/10094)

#### Beta Test with TestFlight

##### New to TestFlight?
- TestFlight is an essential tool to help you distribute and install beta versions of your apps.

    - You can create your teams of testers, define distribution rules, and incorporate feedback to create best-in-class applications for the App Store.

    - To manage your beta testing, go to the App Store Connect website.

    - Check the TestFlight tab, where you can create groups, add testers, and distribute builds.

    - You can also manage testers and groups using App Store Connect on iOS or the App Store Connect API.

    - To get a general overview about how to run your beta program, check out our Tech Talk on how to [Get started with TestFlight](https://developer.apple.com/videos/play/tech-talks/110343)

    - For more information on how to automate distributing builds in continuous integration services, watch our previous session ["Explore Xcode Cloud workflows."](https://developer.apple.com/videos/play/wwdc2021/10268)

- TestFlight is available for all existing operating systems and provides a consistent experience for installing beta apps.

    - Additionally, testers can send screenshots and crash feedback on iOS and macOS.

    - And today we are introducing support for xrOS.

    - TestFlight on xrOS will help you test your immersive apps to make sure they offer the best possible experience on the device and are ready for the App Store.

    - It also lets you install and run iPad and iPhone apps to verify they are fully compatible and work great on xrOS.

    - In this section, I will walk you through the major use cases of TestFlight to help you distribute builds, install apps, and collect feedback.

##### Let's start with distributing builds.

- Creating groups and inviting testers is a feature available for all platforms. It's no different for xrOS.

    - You have an option to use internal or external groups and invite testers by email or public link.

    - In this example, the xrOS platform has been added to an existing app record.

    - You can create a new group of testers and start uploading builds there.

    - You can also distribute xrOS builds through any existing group.

        - In this scenario, testers will have access to builds for multiple platforms.

- TestFlight gives you full control over which group can install iOS apps on xrOS.

    - Each group has an option to enable or disable the ability to install iPhone and iPad apps by testers from this group on the headset.

    - This option can help you expand the team of testers while you progress with testing the compatibility of your iOS apps.

##### Install Apps
- Now that you know how to distribute your builds, let me walk you through the process of installing and running beta apps on xrOS as a tester.

    - After launching TestFlight, I can browse all the apps developers invited me to test.

    - My list in the sidebar includes both xrOS and iOS apps that can be installed and tested on my device.

    - Applications not compatible to install are listed in a separate category of iOS-only apps.

    - When a developer invites me to test both the xrOS and iOS version, TestFlight allows me to switch between each type of the app.

        - Toggle at the top of the app page allows me to choose which version I would like to install and test.

        - From this page, I can check the details of each app, review the description, confirm whether the app is compatible with my device.

        - Additionally, I can scroll down the list to App Settings and customize notifications or opt in for automatic updates, in which case all new versions of the app are downloaded and installed automatically by TestFlight on my device.

- Once the beta app is installed, I can launch it directly from TestFlight or from the Home Screen.

    - All beta apps are distinguished by a yellow dot displayed next to the app name, like on other platforms.

    - Compatible iPad and iPhone apps are grouped together in a dedicated folder, where the yellow dot is also presented for beta versions.

    - When I launch the updated app, TestFlight displays information provided by the developer to describe changes in the latest build.

    - This is a good opportunity for the developer to recommend which areas I should focus on while testing the app.

##### Collect Feedback
- Now, let's talk about how you can get feedback from testers about their experience with your apps on xrOS.

    - Testers can send feedback when they notice issues within your app or if they want to suggest some improvements.

    - As a tester, If I want to share feedback with the developer about my experience on xrOS, I can quickly press the Digital Crown and top buttons together to capture screenshots.

        - Next, I open TestFlight, select the app, and touch the Send Feedback button to initiate the process.

        - I start with describing the problem.

        - I attach all the screenshots I have captured to support the feedback.

        - I can crop or annotate images to focus the feedback on the relevant part of the screenshot or to hide any sensitive information.

    - Another situation where I can provide feedback is when the beta app crashes.

        - In this case, TestFlight asks me if I want to send more information to help debug the issue.

        - I can describe what steps caused the crash, and the information will be submitted along with the crash log captured on the device.

        - So far, I have presented how testers can leverage TestFlight on xrOS to install, run beta apps, and share feedback.

- Now let's take a look how App Store Connect and Xcode can help you analyze the data and track tester engagement.

    - You can review all submitted feedback in App Store Connect and Xcode Organizer, with filters to view by platform or a build.

    - You can check the details of each feedback, review screenshots, download crash logs, or open the feedback directly in Xcode Organizer.

    - App Store Connect web and mobile also provide information about how many testers installed and launched a specific version of your app, or how many of them submitted crash or screenshot feedback.

        - This is an excellent tool to track tester engagement.

        - You can analyze the statistics for a specific build or look over a specific group to see the engagement of each tester.

#### Get Ready for the App Store

- With beta testing wrapped up, let's jump back to App Store Connect and put the finishing touches on your app.

- You're able to manage your xrOS apps using the features you've come to expect from App Store Connect, from in-app purchases, to screenshots, to app analytics.

- Let's take a closer look at a feature we've updated for spatial computing, Privacy Nutrition Labels.

    - With the release of xrOS, we added a few new data types that your app may collect.

    - These new data types are relevant for xrOS apps, but they can also be applied to other platforms.

        - In the App Privacy section, check “Environment Scanning” if your app collects data about the user's surroundings, such as mesh, planes, scene classification, or image detection of the user's surrounding.

        - Under the “Body” section, check “Hands” if your app collects data about the user's hand structure and hand movements, and “Head” if your app collects data about the user's head movement.

        - Once your app is published on the App Store, customers can learn from your app's product page about the data types that your app collects and how they are used.

- For more see  ["What's new in App Store Connect"](https://developer.apple.com/videos/play/wwdc2023/10117)
