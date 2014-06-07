#WWDC 2014
TITLE OF SESSION: Writing Energy Efficient Code Part 1

NUMBER OF SESSION: _number_of_the_session_here_

PRESENTED BY: _names_of_the_presenters_


-------------------------------------------------------------------------------
###NOTES
{If you've contributed, add your name, e-mail & URL at the bottom}

Heavy power consuming elements
CPU
Storage
Networking
Graphics

Performance and energy is interrelated
Dynamic and fixed cost
Fixed cost is required for Dynamic cost, condense the dynamic bits together so fixed cost is decreased / compacted

Avoid unneeded work
===============
When did resign active and become active called, pause everything to be energy efficient
Use applicationWillResign notification

(OS X: Occlusion shows visibility of windows or applications, app nap relies on heuristics so tell app nap to never nap while working)
API in Yosemite to schedule arbitrary tasks at a better time so that you can do battery consuming tasks while charged
Schedule with reverse dns identifier and give tolerance for scheduling in seconds.
Set repeat to yes for repeat
use scheduleWithBlock and then call completion handler when completed. Check shouldDefer when system wants you to pause until later.

NSURLSession Background Session lets you create NSUrlSession with request but it puts it out of process and the system daemon controls the download tasks. When app is killed, the daemon continues the download and your relaunched app with the same identifier can get the out of process session back with the downloaded data. 
configuration.discretionary = YES
Automatically picks the best time to do work
Provides bandwidth monitoring and automatic retry 
configuration.timeoutIntervalForResource = (time in seconds)
Sets scheduling window, should be >12h

New, quality of service classes (QoS)
===========================
‘User Interactive' - Main thread, animations
‘User Initiated' - Immediate results
‘Utility' - Long-runing tasks
‘Background' - Not user visible

Improves responsiveness and overall energy efficiency
*insert PhotoMeister 3000 example*
User Interactive: Main Thread, automatic
User Initiated: Thumbnail generation, Image load (on click)
Utility: Image import and conversion
Background: Search indexing

NSOperationQueue has operation.qualityOfService = NSQualityOfServiceUtility;
If set on both operation and queue, higher will be used
if not set, will infer
To change QoS of operation, set a higher QoS operation on the same queue to raise the QoS of all previous operations of that queue
*PhotoMeister*
If person taps on a picture, raise queue priority from importing and display picture.

*insert Feed Reader 9000 User speaker Q&A (first time I've seen/done one*

Debugging QoS
Xcode 6 will show QoS on usage page / energy / CPU and memory page
spindump -timeline to see threads with QoS

Do it less
=======
Energy impact gauge
10% power use = high power draw
Use performance unit tests (new in Xcode 6)
XCTestCase
Minimize timers
timerfires -p application -s -g
-g when killed gives list of timers
specify timer tolerance
Unnecessary drawing kicks graphics hardware  out of low power mode
On mac, flash screen updates (warning, seizure inducing!)
iOS, flash updated regions cocoa touch
Check unnecessary draws
Writes to flash are more energy hungry than reads
Write minimum content necessary
Writes in aggregate for better efficiency
Any I/O will pull devices out of low power states, minimize I/O

---
###REFERENCES
{as documents / sites are referenced add them below}


---
###QUOTES
{collect nice quotes from this session's speaker}


---
###CONTRIBUTORS
{add your name, e-mail address and URL below}

Yichen Cao, ycao@me.com

---
###E-MAIL BOUNCEBACK
{add your e-mail address separated by commas for easy mailing of this text}

ycao@me.com, 

---
###DISCLAIMER
Copyright shared between all the participants unless otherwise stated...
Generic conference template copyright by Tom Coates, tom@plasticbag.org
Additions and Conference.mode by Dominik Wagner, dom@codingmonkeys.de