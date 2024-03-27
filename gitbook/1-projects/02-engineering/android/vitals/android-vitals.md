
[Android vitals on Google Play Console - YouTube](https://www.youtube.com/watch?v=C9MZNEW20B4&ab_channel=AndroidDevelopers)

- An initiative to improve the stability and performance.
- Android Vitals dashboard highlights
	- **Crash Rate**
	- **ANR Rate**
	- Stuck Wake Locks
	- Excessive Wake Ups


App Stability includes but not limited 

- Crash 
	- Crash is an unexpected exit 
	- When the android app crashes, the android terminates the process and displays a dialog to the user. 
	- "Android App Name" has stopped
	- In this situation the user needs to restart the app and everything is started from scratch.
- ANR
	- When UI thread of android app is blocked for too long, then ANR (Android Not Responding)
	- User is provided with two option
		- Wait for the app to complete loading
		- Force Stop the app
	-  Either of the options, the user is stopped from using the app and is usually forced to restart the app



Depending on the root cause there would be different ways to solve the issues.
Some recommendations by google:

- Issue from your logic code
	- Locate your code to fix the issue
	- Implement QA/Testing process to cover your logic code. 
	-  Use the same device model and android version to try to reproduce the issue if possible

- Issue from 3rd party lib
	- Upgrade to the latest version of the libs or consider using the stable version
	- Seek support from library providers

- Issue from Engines
	- Use the stable version of the engine
	- Seek support from the engine forum / community


