# Open new Safari tabs next to the current

Position new tabs to the immediate right of the current tab in Safari on macOS Tahoe 26

<br>

***For tabs opened with URLs***<br><sub>_(except URLs opened from the Edit Bookmarks page or external apps)_</sub>
###
Open Terminal and run the following commands – then restart Safari
~~~flf
defaults write -app safari WBSNewTabPositionPreferenceKey -int 0
~~~
~~~flf
defaults write -app safari WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey -int 1
~~~

<sup>(If the commands gives you  a `Could not write domain` error, [see here](https://github.com/paralevel/bypass-sandbox-in-macos-terminal))</sup>

<br>

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
- <i>In the leftmost panel</i>
8. Click the very hard to see “Add Group” button
9. In the window that opens, set the name to “Safari”, then under “Allowed Applications”, click “Applications”, select Safari and click “Save”
10. Make sure the newly created “Safari” group is selected
- <i>In the middle panel</i>
11. Click the “Add Workflow” button
- <i>In the rightmost panel</i>
12. Set the workflow name to e.g. “New tab”
13. Under “Add Trigger”, click “Keyboard Shortcut”
14. When the red “Recording…” widget appears, press Cmd-T (recommended)
15. Click “New Command” and then in the popup menu, select “Scripting” and then “New Shellscript” (have to use shell script because the current version of Keyboard Cowboy doesn't request the necessary Automation permission when using AppleScript, causing scripts to fail)
16. Click the “Script goes here” field and paste the following
~~~applescript
#!/usr/bin/osascript
tell application "Safari"
	tell front window
		set _new to make new tab at after (get current tab)
		# make sure the 'New tabs/windows open with' settings are applied by using x-safari-https:// as url
		set _url to "x-safari-https://"
		set URL of _new to _url
		# wait until the tab gets a real url, or else the location bar won't be focused when switching to the new tab
		repeat until URL of _new is not _url
			delay 0.2
		end repeat
		set current tab to _new
	end tell
end tell
~~~
17. Press Cmd-W or manually close the Keyboard Cowboy window, which also removes the icon from the Dock – don't press Cmd-Q or the menu bar process quits too
18. Open Safari and check if the keyboard shortcut works
19. The first time the keyboard shortcut triggers the assigned script, click “Allow” in the dialog that opens asking you to allow “Keyboard Cowboy.app” to control “Safari.app”
20. Make Keyboard Cowboy start automatically when you log in – click the menu bar icon and select “Open at Login”

<br>

_In cases where you actually want to open a tab at the end of the tab bar, you can press Cmd-Opt-T or the “+” (New Tab) button in the toolbar_
    
<br>
<br>
<br>
<br>
