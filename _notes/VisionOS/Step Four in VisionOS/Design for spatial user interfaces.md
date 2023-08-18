---
title: Design for spatial user interfaces
---

### [Design for spatial user interfaces](https://developer.apple.com/videos/play/wwdc2023/10076/)

This video provides several key tips on great spatial user interfaces. Learn how your existing screen-based knowledge easily translates into creating great experiences for visionOS. Explore guidelines for UI components, materials, and typography and find out how you can design experiences that are familiar, legible, and easy to use.


#### App icons 1:12

- App icons are familiar but 3D
    - When looked at, they expand
    - System handles this effect by adding specular highlights and shadows
    - Use multiple layers Up to 3
- Each layer is a square image
    - 1024×1024
    - Circular mask is automatic
    - Automatically shadow cast behind foreground layers
    - Keep graphics centered
    - Avoid layers with reduced opacity


#### Materials 2:45

- Apps should be easy to place, to use at any distance, and to view in any lighting condition
    - Windows act as a canvas for UI
        -Avoid opaque windows
            - Too many opaque windows makes UI feel heavy and overwhelming
    - No distinct light and dark mode
        - Lighting in the room influences the UI
- Glass window
    - Sidebars use darker materials
    - Other elements uses lighter materials
    - Inputs that are highlighted might user darker materials
    - Don’t stack lighter materials because it impacts contrast


#### Typography 5:28

![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/TextWeight.jpeg)

- Use Semantic names
- Use Point based unit sytem
- Font weight
    - Modified to be slightly heavier on visionOS
    - Body is semibold by default
    - Extra Large Title Styles
    - Use bolder font weights for legibility

#### Vibrancy 6:55
- Vibrancy Updates in real time
    - Works on top of the glass material
    - Use system components when possible
- Takes advantage of vibrancy by default
    - Three modes:
        - primary: for standard text
        - secondary: for descriptions, footnotes, subtitles
        - tertiary: ?

- Consider using white text or symbols
- For color
    - Use it in a full button rather than just text
    - System colors adjust hue/vibrancy based on background

![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/ColoredButtons.jpeg)

#### Layout 8:12

- Ergonomics
    - Left and right neck motion is easier than up and down
    - Use wider aspect ratios than taller
    - Center important information in your app
- Sizing
    - Use sizes that are easy to target
        - Tap targets should be at least 60x60 points of tappable space.
        - 44 point buttons should have at least 8 points of space around it
        - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/ButtonTargetArea.jpeg)

        - Buttons in stacks should have at least 16 points of space around them
        - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/ButtonsGap.jpeg)
        - Mini buttons like 28 pixel size in section headers may look small but they have at least 60 points of space around them
        - Large and XL buttons require less spacing around them

- Focus feedback
    - Hover effect is automatic
    - Disabled buttons don’t have a hover effect
    - Lists and menus should have 4 points of space for the hover effect
    - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/ButtonContainerGap.jpeg)

    - Same for a lockup like Music.
        - Define a custom region for a single selectable element.
    - Nested elements should have concentric continuous corners.
        - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/NestedCornerRadius.jpeg)

        - inner corner radius + padding = outer corner radius
        - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/OutsideCornerRadiusCalc.jpeg)

    - Every element is concentric to its nested elements to make them feel like it's one thing

#### From screen to spatial 14:11

- Inputs
    - Most interaction happens at a distance
    - Additionally, direct interaction or keyboard / trackpad
    - Use system components
        - see: [Design for spatial input](https://developer.apple.com/videos/play/wwdc2023/10073)
![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/SystemComponents.jpeg)

- Window
    - made of glass material with window bar below

- Tab bar
    - Vertical and fixed on the left side of Windows
    - Avoid having more than 6 items
    - Long looks shows labels for each section (automatic expand & collapse)
![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/TabBarLongLook.jpeg)

- Side bar
    - Used to provide sub navigation from the tab bar

- Ornaments
    - Replaced for segmented controls in iOS
    - Positioned outside the window with depth, at the bottom
    - Great to present toolbars
    - Usually a collection of buttons: Borderless buttons
    - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/OrnamentButtons.jpeg)


    - Examples: Years/Months/Days in Photos, Playback Controls in Music
    - At the bottom: Overlap by 20 points
    - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/OrnamentGap.jpeg)

    - Only hide ornaments when looking at a single piece of content
    - Ornaments can expand or have navigation hierarchy

- Menus and Popover
    - Centered
    - Can expand outside the window
    - Buttons should be selected when the menu or popover is open
        - Avoid using buttons with white backgrounds unless selected because white is the color of the icon
- Sheets
    - Centered
    - Maintain z position of the window and the window pushes back
    - Secondary modal can be used with additional dimming

    - ![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/NestedModals.jpeg)

    - Consider push navigation within modals
    - Close and back buttons should be in the top left
    - "Pushing" a view onto the stack uses "cross dissolve" animation instead of moving to right

- Outside windows
    - Spatial Captures, can be expanded
![](https://www.wwdcnotes.com/images/notes/wwdc23/10076/OutsideViews.jpeg)

![](https://hackmd.io/_uploads/H1qZ3Bnn3.png)

