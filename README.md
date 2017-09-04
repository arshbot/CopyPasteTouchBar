# CopyPasteTouchBar

The purpose of this project was to create a touchBar application where one could view their clipboard in real time on the touch bar at the bottom of the screen.

## Challenges faced
1) It turns out that the touchBar is not intended to be used for standalone applications. Meaning that every application that intends to use the touchBar must make use of an NSWindow. This is used as a means to select a touchBar application to be presented as there is no way to place your app in the control center of the touchBar.

2) The method touchBar uses to present dynamic collections (NSScrubber) does not support individual cell customization. Normally in a tableView or collectionView, a cell is constructed in a datasource method typically `cellForRow`, and in the NSScrubber equivalent, you must return a `NSScrubberItemView` object by using the ironically named `viewForItemAt`. It is ironically named because it seems every upstream link to any view object is barred to return either the touchBar's ViewController or nil. Every attempt to alter the cell's view is unsuccessfuly, from changing the background color to altering the NSFont size of the text. Although the method is titled `viewForItemAt`, you are unable to alter the view in any significant way.

## Attempts to solve these issues
1) The route taken to prevent a window that must be kept open and selected to use the app was to replace the window with a Menu item and to duplicate all the functionality found in the touchBar. This serves to effectively circumvent the issue and the Menu classes provide tools to monitor the keyboard for copy/paste actions.

2) Unfortunately, this problem proved to be unsolvable ([pending a successful stackoverflow answer](https://stackoverflow.com/questions/46029329/how-can-i-change-the-font-size-of-nstextfield-dynamically-to-fit-as-much-of-a-st)). One attempt I made was to replace the `NSScrubberTextItemView` was with it's counterpart `NSScrubberImageItemView`. However, while the overhead of this path was already excessively difficult (I had to overlay an image with text for every cell, change the background view on selection and recreate the image with text for the split second it's selected), NSScrubber either squishes all the images together for an unsavory view or it creates black bars in between the images producing an even more unsavory view.
