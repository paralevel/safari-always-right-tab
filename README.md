# Open tabs to the right of current tab in Safari

Position new tabs to the immediate right of the current tab in Safari on macOS Tahoe 26

<br>

***For tabs opened with URLs***<br><sub>_(except when opened from the Edit Bookmarks page or external apps)_</sub>
###
Open Terminal and run the following commands – then restart Safari
~~~flf
defaults write -app safari WBSNewTabPositionPreferenceKey -int 0
~~~
~~~flf
defaults write -app safari WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey -int 1
~~~

<sup>(If the commands gives you  a `Could not write domain` error, [see here](https://github.com/paralevel/unfull-disk-access-for-terminal))</sup>

To revert to default tab opening behavior:

<sub>

~~~
defaults delete -app safari WBSNewTabPositionPreferenceKey
~~~

~~~
defaults delete -app safari WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey
~~~

</sub>

<br>

***For blank tabs***
###
1. Download Keyboard Cowboy: https://zenangst.github.io/app/keyboardcowboy/index.html
2. Install and launch it<br>
3. On first launch, when the “Choose your configuration” window appears, click “Empty” followed by “Confirm”
4. Click the ”Request Permission” button in the next window
5. In the ”Accessibility Access” dialog that appears, click “Open System Settings”
6. In the System Settings window that opens, enable Keyboard Cowboy.app
7. Click the Keyboard Cowboy icon in the Menu Bar and select “Open Keyboard Cowboy”

_<ol>In the leftmost panel</ol>_

8. Click the very hard to see “Add Group” button
9. In the window that opens, set the name to “Safari”, then under “Allowed Applications”, click “Applications”, select Safari and click “Save”
10. Make sure the newly created “Safari” group is selected
  
_<ol>In the middle panel</ol>_

11. Click the “Add Workflow” button

_<ol>In the rightmost panel</ol>_

12. Set the workflow name to e.g. “New tab”
13. Under “Add Trigger”, click “Keyboard Shortcut”
14. When the red “Recording…” widget appears, press Cmd-T (recommended)
15. Click “New Command” and then in the popup menu, select “Scripting” and then “New Shellscript” (have to use shell script because the current version of Keyboard Cowboy doesn't request the necessary Automation permission when using AppleScript, causing scripts to fail)
16. Click the “Script goes here” field and paste the following
~~~applescript
#!/usr/bin/osascript
tell front window of application "Safari"
	set _new to make new tab at after (get current tab)
	set current tab to _new
	# make sure the 'New tabs/windows open with' settings are applied by using x-safari-https:// as url
	set URL of _new to "x-safari-https://"
end tell
~~~
17. Press Cmd-W or manually close the Keyboard Cowboy window, which also removes the icon from the Dock – don't press Cmd-Q or the menu bar process quits too
18. Open Safari and check if the keyboard shortcut works
19. The first time the keyboard shortcut triggers the assigned script, click “Allow” in the dialog that opens asking you to allow “Keyboard Cowboy.app” to control “Safari.app”
20. Make Keyboard Cowboy start automatically when you log in – click the menu bar icon and select “Open at Login”

<br>

_In cases where you actually want to create a new tab at the end of the tab bar, you can press Cmd-Opt-T or the “+” (New Tab) button in the toolbar_
    
<br>
<br>
<br>
<br>
