# Always Right New Tab in Safari
<sup>_System Requirements: macOS Tahoe 26_</sup>
<br>
<br>
Position new tabs to the immediate right of the current tab in Safari on macOS.
<br>
<br>
***For tabs opened with URLs***
###
Run the following Terminal command and restart Safari afterwards:
<pre><code><tt>defaults write -app safari WBSNewTabPositionPreferenceKey -int 0; defaults write -app safari WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey -int 1</tt></code></pre>
<sub>If you  get a “Could not write domain” error, [see here](https://github.com/paralevel/useful-disk-access-for-terminal)</sub>

<i>
<sub>To revert:</sub>
<pre><code><tt>defaults delete -app safari WBSNewTabPositionPreferenceKey; defaults delete -app safari WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey</tt></code></pre>
</i>

***For blank tabs***
###
 
Since the previous settings don’t apply to new _blank_ tabs, use the following workaround (actually there’s also a <samp>WBSNewBlankTabPositionAppliesToAllBlankTabsPreferenceKey</samp> setting, but enabling it doesn’t seem to do anything, even when enabling the related <samp>WBSTabOrderManagerSuppressRelatingNewBlankTabsPreferenceKey</samp> setting):

1. Download the free and open source [Keyboard Cowboy](https://zenangst.github.io/app/keyboardcowboy/index.html)
2. Install and launch it
3. On first launch, when the “Choose your configuration” window appears, click “Empty” followed by “Confirm”
4. Click the ”Request Permission” button in the next window
5. In the ”Accessibility Access” dialog that appears, click “Open System Settings”
6. In the System Settings window that opens, enable “Keyboard Cowboy.app”
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
14. When the red “Recording…” widget appears, press <kbd>command</kbd> <kbd>T</kbd> (recommended)
15. Click “New Command” and then in the popup menu, select “Scripting” and then “New Shellscript” (have to use shell script because the current version of Keyboard Cowboy doesn't request the necessary Automation permission when using AppleScript, causing scripts to fail)
16. Click the “Script goes here” field and paste the following
~~~applescript
#!/usr/bin/osascript
tell front window of application "Safari"
	set _new to make new tab at after (get current tab)
	set current tab to _new
	set URL of _new to "favorites://"
end tell
~~~
17. Close the Keyboard Cowboy window to remove it from the Dock – do _not_ press <kbd>command</kbd> <kbd>Q</kbd> or the menu bar process quits too!
18. Open Safari and check if the keyboard shortcut works
19. The first time the keyboard shortcut triggers the assigned script, click “Allow” in the dialog that opens asking you to allow “Keyboard Cowboy.app” to control “Safari.app”
20. Make Keyboard Cowboy start automatically when you log in – click the menu bar icon and select “Open at Login”

(In case you actually *want* to create a new tab at the end of the tab bar, you can always press <kbd>command</kbd> <kbd>option</kbd> <kbd>T</kbd> or the “+” button in the toolbar)
