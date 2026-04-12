# Always position new tabs to the immediate right of the current tab in Safari on macOS Tahoe 26

<br>

***For tabs opened from links***<br><sub>_(except when opened from the Edit Bookmarks page)_</sub>

<br>

Open Terminal and run the following commands – then restart Safari
~~~flf
defaults write $HOME/Library/Containers/com.apple.Safari/Data/Library/Preferences/com.apple.Safari.plist WBSNewTabPositionPreferenceKey -int 0
~~~
~~~flf
defaults write $HOME/Library/Containers/com.apple.Safari/Data/Library/Preferences/com.apple.Safari.plist WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey -int 1
~~~

<br>

<sup>
<i>

To revert:
~~~
defaults delete $HOME/Library/Containers/com.apple.Safari/Data/Library/Preferences/com.apple.Safari.plist WBSNewTabPositionPreferenceKey
~~~
~~~
defaults delete $HOME/Library/Containers/com.apple.Safari/Data/Library/Preferences/com.apple.Safari.plist WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey
~~~

</i>
</sup>

<br>

***For blank tabs***

<br>

<ol>
  <li>Download Keyboard Cowboy: https://zenangst.github.io/app/keyboardcowboy/index.html
<br /><br />
  </li><li>Install and launch it
<br /><br />
    <ins><i>Once opened, in the leftmost panel</i></ins>
<br /><br />
  </li><li>Under <i>Configuration</i>, leave it at <i>Default</i> <i>Configuration</i>
<br /><br />
  </li><li>Under <i>Groups</i>, click the barely visible <i>Add</i> <i>Group</i> button
<br /><br />
  </li><li>In the window that opens, set the name to <i>Safari</i>, then in the <i>Application</i> drop-down menu, select Safari, and finally click <i>Save</i>
<br /><br />
  </li><li>Make sure the <i>Safari</i> group is selected
<br /><br />
    <ins><i>In the middle panel</i></ins>
<br /><br />
</li><li>Under <i>Workflows</i>, click the barely visible <i>Add</i> <i>Workflow</i> button
<br /><br />
  <ins><i>In the rightmost panel</i></ins>
<br /><br />
  </li><li>Set the workflow name to e.g. <i>New</i> <i>tab</i>
<br /><br />
  </li><li>Under <i>Add</i> <i>Trigger</i>, click the <i>Keyboard</i> <i>Shortcut</i> button
<br /><br />
  </li><li>Use command-T (recommended) as the keyboard shortcut
<br /><br />
  </li><li>Click the <i>New</i> <i>Command</i> button and then in the popup menu, select <i>Scripting</i> and then <i>New</i> <i>AppleScript</i>
<br /><br />
  </li><li>Set name of the script to e.g. <i>New</i> <i>tab</i> <i>script</i>
<br /><br />
  </li><li>Click the <i>Script goes here</i> field and paste the following
  
~~~applescript
tell application "Safari"
	tell front window
		set _new to make new tab at after (get current tab)
		# make sure the 'New tabs/windows open with' settings are applied by using x-safari-https:// as url
		set _url to "x-safari-https://"
		set URL of _new to _url
		# wait until the tab gets a real url, or else the location bar won't be focused when switching to the new tab
		repeat until URL of _new is not _url
			delay 0.5
		end repeat
		set current tab to _new
	end tell
end tell
~~~
  
  </li><li>Open Safari and check if the keyboard shortcut works
<br /><br />
  </li><li>Make Keyboard Cowboy start automatically when you log in – click the menu bar icon and select <i>Open</i> <i>at</i> <i>Login</i>
<br /><br />
  <ins><i>Optionally also</i></ins>
<br /><br />
  </li><li>In the leftmost panel in Keyboard Cowboy, go into every group and disable all the default workflows, since some of them have keyboard shortcuts as triggers that you might not like
<br /><br />
  </li><li>To get rid of the Dock icon, click the icon and then in the open Keyboard Cowboy window, press command-W or click the red <i>close</i> button in the top-left corner (don't press command-Q, or the background process too gets terminated)
<br /><br />
  </li><li>In Safari, right-click the toolbar, choose <i>Customize</i> <i>Toolbar</i> and drag the +/New Tab button out of the toolbar, since it opens the tab at the end of the entire tab bar
  </li></ol>
<br/>
