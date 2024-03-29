---
title: What’s new in Safari extensions
---

### [What’s new in Safari extensions](https://developer.apple.com/videos/play/wwdc2023/10119/)

The next step Apple suggest is to learn about the Safari, lets check out how spatial computing changes web browsing.

"Learn about the latest improvements to Safari extensions. We'll take you through new APIs, explore per-site permissions for Safari app extensions, and share how you can make sure your extensions work great in both Private Browsing and Profiles."
-Apple


#### Overview
- There are four ways to build Safari extensions: content blockers, share extensions, app extensions, and web extensions.

- Safari 17 continues to support all of these types, but the future of browser customization lies in web extensions.

    - Apple is dedicated to standardizing web extensions alongside the other major browser vendors.

        - This collaboration aims to improve compatibility, streamline development, and ensure a familiar experience across all browsers.

        - We're working together in the W3C WebExtensions Community Group, where Apple proudly serves as a cochair.

        - By connecting with other browser and extension developers to drive this standardization effort, we're building a stronger and more unified web extension ecosystem.

- Before jumping into today's topics, I'd like to share two key details about Safari web extensions.

    - First, Safari 17 will continue to support both Manifest v2 and v3 web extensions.

        - We'll continue to add new features to Manifest v3, so update when it makes sense for your extension.

    - Second, web extensions are the best way to build extensions for Safari across platforms.

        - With a single shared codebase, web extensions allow you to customize the capabilities of Safari on iOS, iPadOS, macOS, and now xrOS.

        - That's right, web extension available on iOS and iPadOS will also be available on xrOS.

        - Web extensions on xrOS work just like you'd expect and have the same capabilities as extensions on iOS, including the ability to inject scripts, run background content, and display popovers.

        - We're excited to see how your extensions enhance the browsing experience on xrOS.

- To learn more about Safari on xrOS, check out [[Meet Safari for xrOS]] With those announcements out of the way, here's what we'll cover in the rest of today's session.






#### APIs
- Content blockers are a great way to clean up web pages, remove annoyances, and block loading of scripts.

    - Content blockers use rules defined in JSON to block or hide content without needing access to any information about what websites are visited.

    - Declaratively hiding content on web pages can be tricky.

    - That's why content blockers now support :has() selectors.

        - :has() selectors are great because they allow your content blocker to precisely target parent elements based on their children.

        - In this rule example, we're hiding any elements with the class .post that also have a child element with the class .paid-promo.

        - Extensions that hide webpage content, or block network requests, are some of the most popular types of extensions.

        - That's why Safari continues to support you in creating innovative and effective extensions that offer a secure and private browsing experience for your users.

- If you're looking to block or modify network requests with a web extension, you should check out these updates to Declarative Net Request.

    - Declarative Net Request is a powerful API that provides a way for your web extension to block and modify network requests.

    - Like content blockers, your extension provides rules in a JSON format and Safari handles the rest.

        - This means enhanced power efficiency, especially on battery-powered devices.

            - Since these rules are declarative, your extension doesn't need access to webpages the user visits, increasing their privacy and security.

    - One big update to Declarative Net Request in Safari 16.4 is that your extension can now modify request headers.

        - In this example, I've defined an action that sets a custom User-Agent header for all requests made to example.com.

        - Beyond setting headers, this action type can modify headers by adding new values, removing existing values, or even removing headers entirely from HTTP requests.

- Modifying network requests is a powerful tool, and there are some key points to keep in mind.

    - First, you must declare the declarativeNetRequestWithHostAccess permission in the manifest.

    - In Safari 16.4, this permission is now also required for redirect actions.

    - Your extension must also be granted per-site permissions for any modify headers or redirect actions to be applied.

    - This ensures that the user has control over their data on a site-by-site basis.

        - By keeping these considerations in mind, you can create powerful and privacy-friendly content-blocking extensions that provide a tailored experience for your users.

- If you're building an extension that uses Declarative Net Request, you may want to let your users know just how many requests it has blocked.

    - Using the new declarativeNetRequest.setExtensionActionOptions API, you can configure the badge text to display action counts, such as the number of blocked loads.

    - In this example, we set the displayActionCountAsBadgeText option to true, which is currently the only option for this API.

    - Your extension badge will update automatically based on the actions taken.

    - This allows your users to easily monitor the extension's activity and effectiveness, all while keeping their browsing history private.

- Now I'll cover an update to the scripting API that gives you more control over the behavior of your extension.

    - With the registerContentScript set of APIs, you can create content scripts that can be registered, updated, or removed programmatically.

    - This means that you can target specific pages or conditions to apply to content scripts.

    - In this example, I'm registering a script to be injected onto pages that match webkit.org.

    - This script registration will also persist across sessions.

        - This new API complements the static content scripts defined in the extension manifest, giving you greater flexibility in managing content scripts and enabling you to create more advanced features for your extensions.

##### Temporary session storage
- Safari 16.4 also brings a new storage area to web extensions: the session storage area.

    - Storing and retrieving data from session storage uses the same familiar functions as other storage areas.

    - This API allows you to store data in memory for the duration of your browser session, providing a fast and efficient way to access data between nonpersistent background page loads.

    - Unlike local storage, session storage is not persisted to disk and it's cleared when Safari quits.

- This makes session storage particularly useful for storing sensitive or security-related data, such as decryption keys or authentication tokens, that should not be stored in local storage.

##### Icons
- Finally, we know that making sure your extension has all the right icon sizes for different UI elements is a chore.

    - That's why starting in Safari 16.4, you can now create a single SVG icon that looks beautiful at any size.

    - Safari will take care of scaling your extension's icon sharply, letting you focus on everything else.

    - Those API updates are just some of the improvements to Safari extensions this year.


#### Safari app extensions and per-site permissions.
- Now let's talk about Safari app extensions and per-site permissions.
- If you're already familiar with per-site permissions from web extensions, they work the same way for app extensions.
- Users are able to grant extensions access to websites as they browse, providing for better privacy and control.
- When an extension is first turned on, it won't have access to any sites that the user visits.

- The first time an extension tries to access the page, Safari will badge the extension's toolbar item alerting the user that the extension wants access to the current page.

    - When the user clicks on that toolbar item, they'll be shown information about what access the extension will have, and be given the option to Allow for One Day, or Always Allow.

    - When granted permission, the extension's toolbar item will be tinted to show that the extension has access to the current page.

- Anyone that upgrades to Safari 17 and already has Safari app extensions turned on will have all permissions migrated for those extensions.

- They'll also be shown a banner giving them the option to increase their privacy.

- If Ask for Each Website is chosen, all Safari app extension permissions will be reset, and your users will be able to grant your extension access to each site as they visit.

- There are no new APIs to adopt to support this change in Safari 17; however, take some time to review your extension's assumptions and test how your extensions behave in Safari 17.

- Your users will have full control over the websites every Safari app extension can access.

- Your extension will automatically have access to sites when permission is granted by the user.

- However, permissions can be granted or revoked at any time.

- Toolbar items are now shown by default for all extensions.

    - Take a look at how your extension icon appears in Safari and supply a PDF vector icon that can be tinted appropriately.

#### Safari Profiles and Private Browsing.
- Finally, let's talk about updates to how extensions work in both Profiles and Private Browsing.

- In Safari 17, users will be able to control which extensions have access to their Private Browsing windows and tabs without needing to turn off the extension in other browsing contexts.

- Extensions that inject scripts, or can read information about the pages a user visits, are turned off by default.

- However, extensions that don't access content, like content blockers, are automatically allowed in Private Browsing because there aren't any additional privacy concerns.

- Here's the updated Extensions pane in Safari settings on macOS and there are similar updates on iOS.

    - There's a new option to allow this extension in Private Browsing.

    - For extensions that are turned on, it's one click in Safari settings to allow that extension access to Private Browsing as well.

##### Profiles
- Profiles are new in Safari this year.

- They're a way to keep browsing data separated.

    - Profiles contain separate history, cookies, and website data.

    - Users can also choose which extensions they want to turn on per profile.

    - This includes new tab page extensions.

    - And of course, all these settings sync across all of a user's iPhone, iPad, and Macs through iCloud.

- The Extensions pane in Safari settings has also been updated to list the profiles where an extension is active.

    - Here you can see that the Sea Creator extension is active in both Work and School profiles.

    - When an extension is turned on in a profile, it is an entirely new instance of that extension.

    - This means each instance will have a different UUID, background page, and storage.

- However, per-site permissions are shared across profiles.

    - That means your users only need to grant your extension access once.

    - When running in a profile, an extension only has access to the windows, tabs, and other data related to that profile.

    - If your extension communicates with a native host app, make sure that your app expects to receive messages from multiple profiles and respects the separation of data across those profiles.

        - When your app receives a call to beginRequest(with context:), decode the userInfo dictionary.

        - If your extension is active in a profile, there will be a profileIdentifier value for the key SFExtensionProfileKey.

        - Since extensions have unique instances per profile, it's possible to inspect their background content separately.

###### Inspecting background content
- From the Develop menu in Safari 17, you can dive into the Web Extension Background Content menu item and see the background pages and service workers grouped by extension.

    - Each extension will list its inspectable content per profile.

    - To learn more about the improvements to Safari developer features this year, check out [What's new in Web Inspector](https://developer.apple.com/videos/play/wwdc2023/10118) and [Rediscover Safari developer features](https://developer.apple.com/videos/play/wwdc2023/10262).
    -  In summary, Safari is committed to standardizing web extensions and providing you with new APIs to create innovative and effective extensions.
