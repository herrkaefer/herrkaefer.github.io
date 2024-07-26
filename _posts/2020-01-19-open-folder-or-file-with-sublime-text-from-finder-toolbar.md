---
layout: post
title: Open folder or file with Sublime Text from Finder toolbar
date: 2020-01-19
category: Workflow
tags: macOS, Finder, workflow, SublimeText
summary: How to open folder in Sublime Text directly from Finder?
published: true
---

<img src="/assets/images/open-with-sublime.png" style="zoom:100%;" />

## Solution

Make a light-weighted application with AppleScript.

### Step 1

Create a new AppleScript script, input:

```applescript
try
	tell application "Finder"
		set sel to selection
		set numElements to count sel
		if numElements is 1 then
			set itemPath to POSIX path of (sel as string)
		else
			set itemPath to POSIX path of ((folder of the front Finder window) as alias)
		end if
		tell application "Terminal"
			do shell script "/usr/local/bin/subl " & quoted form of itemPath
		end tell
	end tell
on error
	log "Error: No selection"
end try
```

- Export it as an application. 
- Move it to "Application" folder. 
- Cmd + Drag it to Finder's toobar.

### Step 2:

Open System Preferences > Security & Privacy > Privacy > Accessibility, add your app to the list.