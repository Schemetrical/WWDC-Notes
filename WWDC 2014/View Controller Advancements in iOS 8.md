#WWDC 2014
TITLE OF SESSION: View Controller Advancements in iOS 8

NUMBER OF SESSION: _number_of_the_session_here_

PRESENTED BY: _names_of_the_presenters_


-------------------------------------------------------------------------------
###NOTES
{If you've contributed, add your name, e-mail & URL at the bottom}

Before iOS 8
Device Type
Interface Orientation
Size

iOS 8 and Later
Traits and trait collections
Size

2 size classes
Idiom
Scale

iPhone 
Vertical is x Compact y Regular
Horizontal is x Compact y Compact

iPad
Vertical is x Regular y Regular
Horizontal is x Regular y Regular

UISVC
=====
Master VC is x Compact

traitCollectionDidChange:
(void) setOverrideTraitCollection: forChildViewController:

Split view collapse and expand
When expanded, you can still push the master ‘off screen' but when collapsed, you can click the back button to go back to master but cannot put a master in. 

To do that, use setOverrideTraitCollection
And set preferred display mode so that the bar shows
Enum from auto, hidden, visible, and overlay
Most of API deprecated  and replaced by new API
Control display width for preferredPrimaryColumnWithFraction to control individual split views. Also can set max and min and get values of actual width.

Hide-able bars for tapping and condensing like safari
condensesBarOnSwipe, hideBarsOnTap

Custom Presentations
================
iOS 7
Ask transition delegate to get animation controller
Limitations:

iOS 8
Get new object PresentationController
it asks the AnimationController and PresentationController presents itself
viewForKey to find views participating in animation
<UIAppearanceContainer, UITraitEnvironment, UIContentContainer>

Previous iPad only styles are available on the iPhone but adapt to full screen presentation. 
UIModalPresentationOverFullscreen;
UIModalPresentationOverCurrentContext;
UIModalPresentationPopover;
UIPopoverController slowly deprecating >
Use Popover presentation
FormSheet
PageSheet
Popover
Custom
Default to fullscreen on compact environments
Able to change adaptation and override
adaptivePresentationStyleForPresentationController:
presentationController:viewControllerForAdaptivePresentationStyle:
UIPopoverPresentationControllerDelegate

New popover API
Set modal presentation style to popover
get the popoverPresentationController (Before presented)
specify everything for popover
present
(Very ugly! Popover on iPhones without config is uglie)
Underlaps the status bar
Looks very bad
No way to dismiss the popover
So go to presentation controller delegate
set the presentation to UIModalPresentationOverFullscreen
use UIVisualEffectView
Adjust content
Add navigation bar and add dismiss bar
Adaptive but still uglie :(
set adaptive to none
Actual popover (ON IPHONE!)
*Audience applauds finally*

All presentation has presentation controller
To create presentation controller, adapt = full screen for iPhone, return no to use same presentation

“For the self aware App, a device rotation is only an animated bounds change" - Anonymous (heh)

willRotateToInterfaceOrientation etc deprecated :p
*applause*
instead viewWillTransitionToSize:withTransitionCoordinator:
(CGAffineTransform)targetTransform
legacy rotation methods still available
viewWillTransform:toSize propagate through entire hierarchy 
call super to propagate to all view controllers

animateAlongside:withTransitionCoordinator:
transition coordinator, can perform an invert alongside block to counterrotate screen elements

Screen Coordinates
===============
iOS 7
Screen orientation fixed to top left (fixed coordinate system) even though interface orientation is different

iOS 8
UIScreen is now interface orientation
UICoordinateSpace protocol (not in seed 1)
@property coordinateSpace
@property fixedCoordinateSpace
convertToCoordinate to convert to and fro


---
###REFERENCES
{as documents / sites are referenced add them below}


---
###QUOTES
{collect nice quotes from this session's speaker}


---
###CONTRIBUTORS

Yichen Cao, ycao@me.com

---
###E-MAIL BOUNCEBACK

ycao@me.com, 

---
###DISCLAIMER
Copyright shared between all the participants unless otherwise stated...
Generic conference template copyright by Tom Coates, tom@plasticbag.org
Additions and Conference.mode by Dominik Wagner, dom@codingmonkeys.de