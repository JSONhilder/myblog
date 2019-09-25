---
title: "My_windows"
date: "2019-09-23"
draft: true
image: "imgs/"
description: 
tags: ["WindowsOS", "Development", "OS set up"]
type: "post"
---

# Setting Up A Fast And Reliable Windows OS

Windows OS

ORDER OF PRIORITY
-*-*-*-

Install Graphics Drivers
------------------------------------------------------------------------------------------------------------

Setup Dual Screens
------------------------------------------------------------------------------------------------------------

Change update chanel off of targeted.
check for updates > advanced settings > Choose when updates are installed

Then change delivery optimizaion settings
disable "allow downloads from other pcs"

Optional you can also disable automatic updates completely but I am not going to.
------------------------------------------------------------------------------------------------------------

Stop telemetry with shutup10
https://www.oo-software.com/en/shutup10
Could need to run the app a few times after restart, also check every few weeks!
------------------------------------------------------------------------------------------------------------

Remove unneeded apps/software with github bloat remover script
https://www.christitus.com/2018/09/09/debloat-windows-10/  (to do steps)
------------------------------------------------------------------------------------------------------------

Adjust Privacy settings 
Settings > Privacy > 
	general - all off
	speech - off
	inking & typing - off
	diagnostics - basic and off - feedback frequency - Never
	Activity History - off
	Location - off 
	background applications - all off
	app diagnostics - all off
------------------------------------------------------------------------------------------------------------

Remove Hard drive file indexing
this pc > HDD with OS installed > right click > properties > bottom option allow files... uncheck 
Let it finish
------------------------------------------------------------------------------------------------------------

Set up Mozilla Firefox and Chrome
------------------------------------------------------------------------------------------------------------

Install and setup Vscode:
 extensions:
  + python
  + Pylingo
  + material icon theme
  + Markdown All in One
  + live server
  + indent rainbow
  + Code Runner

 + custom settings > ctrl+shift+p > "show settings (JSON)"
	then paste:
		{
		    "workbench.iconTheme": "material-icon-theme",
		    "workbench.colorTheme": "Firefox Dark",

		    "editor.cursorBlinking": "smooth",
		    "editor.cursorSmoothCaretAnimation": true,
		    "editor.cursorStyle": "block",

		    "editor.fontFamily": "",
		    "editor.fontLigatures": true,
		    "editor.fontSize": 17,
		    "editor.fontWeight": "500",

		    "editor.formatOnPaste": true,

		    "telemetry.enableTelemetry": false,

		    "workbench.editor.highlightModifiedTabs": true,
		}
------------------------------------------------------------------------------------------------------------

Download and sync Mega
------------------------------------------------------------------------------------------------------------

Set up environment variables and aliases
------------------------------------------------------------------------------------------------------------

install python3.7
Make sure to set path to windows as well as change install location to c drive under Python
------------------------------------------------------------------------------------------------------------

Install Git
	-Generate and add github sshkey
------------------------------------------------------------------------------------------------------------

Install windows subsystem for linux
Control Panel > Programs and Features > Turn Windows features on or off > scroll to Windows Subsystem fro Linux
------------------------------------------------------------------------------------------------------------

Install Visual Studio