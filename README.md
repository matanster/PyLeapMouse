PyLeapMouse
===========

Forked from https://github.com/openleap/PyLeapMouse. See there for earlier inspirations. 
Works with Linux, OS X and Windows, but this fork is only tested for Linux. I tried improving the setup instructions but admittedly they're still a bit vague for newbs. If you'd like to add more specific details (that are still generic) please let me know.

###Small word of advice for making changes to the code:
For making changes, see https://github.com/matanster/PyLeapMouse/blob/master/PalmControl.py for starters.

###Performance impact
Note that the Leap may consume a full single CPU (on Linux) when interaction in its sensed cube area is anywhere above moderately intense. Surely you have more than a single CPU but it's nice to be aware of this impact.

###Setup 
0. Download and install the Leap SDK for your platform
1. Start the leap software 
2. Clone this repo
3. Plug in your Leap, test that it seems well calibrated using it's Diagnostic Visualizer menu option
3. WINDOWS USERS: You must copy the Leap.py file and all required library files (.libs and .dlls) from your Leap SDK folder to the "Windows" folder of this repo. These files are already included for OS X users, because OS X is 64-bit only.
4. LINUX USERS: You must copy the `Leap.py` file and all required library (`.so`) files from your Leap SDK folder to the "Linux" folder of this repo (same reason as for Windows); alternatively, add the directory (or directories) containing them to your PYTHONPATH. 
5. You must have the `PyUserInput` and `Xlib` Python modules installed. A google search will get you there..
###Starting and stopping
6. To launch, on Linux, change directory into the cloned repo, and run `start.sh`. For other platform clone and tweak this script to match your OS

###Usage
Operation is as follows:
One hand in frame: The tilt of this hand moves the mouse.
Two hands in frame: Left hand controls action.
    All fingers closed: Mouse movement with right hand tilt.
    One finger open: Clicking. Left mouse button is down. Mouse movement with right hand tilt.
    Two fingers open: Scrolling. Scrolling with right hand movement.
This is a somewhat unintuitive method of operation, but I find that it gives exceptionally better control than the most obvious "point-at-screen" method of mouse control. With this two-handed tilt based mode, it is easy to hit and properly engage small buttons, scroll through webpages, etc.

###Usage with Motion Mode (python PyLeapMouse.py --motion):
Movements are associated with commands listed in a file `commands.ini` placed at the root folder. Here is an example of what the file should look like :

    [screentap]

    [keytap]

    [swiperight]
    1finger: rhythmbox-client --next
    2finger: rhythmbox-client --next
    3finger: rhythmbox-client --next
    4finger: rhythmbox-client --next
    5finger: rhythmbox-client --next

    [swipeleft]
    1finger: rhythmbox-client --previous
    2finger: rhythmbox-client --previous
    3finger: rhythmbox-client --previous
    4finger: rhythmbox-client --previous
    5finger: rhythmbox-client --previous

    [clockwise]
    1finger: rhythmbox-client --play
    2finger: rhythmbox-client --play
    3finger: rhythmbox-client --play
    4finger: rhythmbox-client --play
    5finger: rhythmbox-client --play

    [counterclockwise]
    1finger: rhythmbox-client --pause
    2finger: rhythmbox-client --pause
    3finger: rhythmbox-client --pause
    4finger: rhythmbox-client --pause
    5finger: rhythmbox-client --pause

Every commands could have a different behaviour if 1, 2, 3 ... 10 fingers are recognized but It's recommanded to use the same command for each number of fingers due to a lack of precision with Leap Motion.

###Notes:
This is a spare-time project, so it's not perfect quality. However, I tried to keep the code clean and readable. Let me know if you find any bugs (which there are certainly at least a few of). You can reach me at  will (dot) yager (at) gmail (dot) (what the gmail domain ends in).
The contents of the files are as follows:
PyLeapMouse.py: The actual program
FingerControl.py: Pointer-finger-control specific code
PalmControl.py: Palm-tilt-control specific code
Linux/OSX/Windows:
    Various OS-specific Leap library files
    Mouse.py: A set of generic commands and classes to abstract away from OS-Specific mouse commands
Geometry.py: Geometric functions
MiscFunctions.py: Things that aren't strictly geometry and aren't specific to any interface style
README.md: You are here

###Advanced Options:
`--smooth-aggressiveness [value]` sets the number of samples to use for pointer finger mouse smoothing.
`--smooth-falloff [value]` sets the rate at which previous samples lose importance.
For every sample back in time, the previous location of the mouse is weighted with weight smooth_falloff^(-#sample).
So if smooth_falloff = 1.2, the current frame has weight 1/(1.2^0)=1, but the frame from 5 frames ago has weight 1/(1.2^5) = .4
By default, the smooth aggressiveness is 8 frames with a falloff of 1.3.

