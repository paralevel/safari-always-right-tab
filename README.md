# Always position new tabs to the immediate right of the current tab in Safari on macOS Tahoe 26

<br>

***For tabs opened with URLs***<br><sub>_(except when opened from the Edit Bookmarks page)_</sub>

<br>

Open Terminal and run the following commands – then restart Safari
~~~flf
defaults write -app safari WBSNewTabPositionPreferenceKey -int 0
~~~
~~~flf
defaults write -app safari WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey -int 1
~~~

<sub>_Workaround if you get a `Could not write domain` error (a bug that happens on new macOS installations or on newly created user accounts, when `com.apple.Safari.plist` hasn't been initialized yet):_</sub>
<br>
<sub>_`open $HOME/Library/Containers/com.apple.Safari/Data/Library/Preferences/`_</sub>
<br>
<sub>_`defaults read `\<drag and drop `com.apple.Safari.plist` from Finder here\>_</sub>
<br>
<sub>_Run the commands again_</sub>

<br>

<sub>_To revert:_</sub>
<br>
<sub>_`defaults delete -app safari WBSNewTabPositionPreferenceKey`_</sub>
<br>
<sub>_`defaults delete -app safari WBSNewTabPositionAppliesToSpawnedTabsPreferenceKey`_</sub>

<br>
<br>

***For blank tabs***

<br>

<ol>
  <li>Download Keyboard Cowboy: https://zenangst.github.io/app/keyboardcowboy/index.html
<br /><br />
  </li><li>Install and launch it
<br /><br />
    <ins><i>In the leftmost panel</i></ins>
<br /><br />
	</li><li>When the “Choose your configuration" window appears, click “Empty" and “Confirm”
<br /><br />
		</li><li>Click the ”Request Permission" button in the next window
<br /><br />
	</li><li>In the ”Accessibility Access" dialog that appears, click “Open System Settings”
<br /><br />
	</li><li>In the System Settings window, check Keyboard Cowboy.app
<br /><br />
		</li><li>Click the Keyboard Cowboy icon in the Menu Bar and select “Open Keyboard Cowboy”
<br /><br />
  </li><li>In the left panel, click the very hard to see “Add Group” button
<br /><br />
  </li><li>In the window that opens, set the name to “Safari”, then under “Allowed Applications". click “Applications”, select Safari and click “Save”
<br /><br />
  </li><li>Make sure the newly created “Safari” group is selected
<br /><br />
    <ins><i>In the middle panel</i></ins>
<br /><br />
</li><li>Click the “Add Workflow”
<br /><br />
  <ins><i>In the rightmost panel</i></ins>
<br /><br />
  </li><li>Set the workflow name to e.g. “New tab”
<br /><br />
  </li><li>Under “Add Trigger”, click “Keyboard Shortcut”
<br /><br />
  </li><li>When the red “Recording…” widget appears, press Command + T (recommended)
<br /><br />
  </li><li>Click “New Command” and then in the popup menu, select “Scripting” and then “New Shellscript” (have to use shell script since the current version of Keyboard Cowboy fails to ask for Automation permission when using AppleScript)
<br /><br />
  </li><li>Click the “Script goes here” field and paste the following
  
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

   </li><li>Press Command + W or manually close the Keyboard Cowboy window, which also removes the icon from the Dock – don't press Command + Q or the Menu Bar process quits too
<br /><br />
  </li><li>Open Safari and check if the keyboard shortcut works
<br /><br />
	   </li><li>The first time the keyboard shortcut triggers the assigned script, click "Allow" in the dialog that opens asking you to allow “Keyboard Cowboy.app” to control “Safari.app”
		   <br /><br />
  </li><li>Make Keyboard Cowboy start automatically when you log in – click the menu bar icon and select “Open at Login</i>
<br /><br />
  <ins><i>Optionally also</i></ins>
<br /><br />
  </li><li>In Safari, right-click the toolbar, choose <i>Customize</i> <i>Toolbar</i> and drag the +/New Tab button out of the toolbar, since it opens the tab at the end of the entire tab bar
  </li></ol>
<br/>
