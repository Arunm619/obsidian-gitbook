[Revolutionizing ANR Detection at Sentry - droidcon](https://www.droidcon.com/2023/08/01/revolutionizing-anr-detection-at-sentry/)


Sentry 

- App monitoring tool in production 
- Developer tools by devs for devs
- Open source 
- Free* (self hosting)

Android/ iOS/ React native/ Kotlin Multi platform 

- Enriching crashes with metadata 
- Screenshots 
- Bread crumbs (logs prior to exceptions)
- View heirarchy 
- Performance products 
	- TTD
	- TTFD
- Profiling 
- ANR detection 


ANR detection History 



What is ANR?

ANR dialog -> APP NOT RESPONDING 
 Either wait or Close 

ANR types 
1. `Input dispatching timeout (Activity) : app doesn't respond to input event for 5 seconds` 
2. Executing Service: 
	1. Foreground: not calling `startForeground()` for 10 seconds 
	2. Regular: not finishing `onCreate()` / `onStartCommand()` / `onBind()` within 20 seconds. 
3. Broadcast receiver: not finishing `onReceive()` within 10 seconds 


Android vitals 
Android vitals can help you monitor and improve app's ANR rate. Android vitals measure several ANR rates. 

ANR rate: the percentage of your daily active users who experienced any type of ANR. 
User-perceived ANR rate: The percentage of your daily active users who experienced atleast one user-perceived ANR. Currently only ANRS of type `Input dispatching timed out` are considered user-perceived. 


It will affect app ranking on playstore. 
Threshold is 0.47%


Application.onANRdetected() X missing from Android SDK. 


ANR detection mechanisms 

1. Watch dog thread : periodically send a task to the main thread and checks if it gets executed within 5 seconds. 
2. Native signal handler : install native `SIGQUIT` handler and wire it over `JNI`
3. `ApplicationExitInfo` : Use system API to retrieve ANRs on next app launch. 


Watch dog 

pros: 
1. Almost real-time reporting 
2. Ability to enrish ANR events with current state of the devices (battery level, available memory, screenshot, etc)
3. Available on all android versions. 

cons: 
1. A lot of false positives 
2. No Service or Broadcast receiver ANRs detections 
3. Little thread info (no deadlock detection)


Native signal handler 

 pros: 
1. Almost real-time reporting 
2. Ability to enrish ANR events with current state of the devices (battery level, available memory, screenshot, etc)
3. Available on all android versions. 

cons: 
1. False positives 
2. No background ANR detection 
3. Little thread info (no deadlock detection)



ApplicationExitInfo 

Pros: 
1. Most accurate ANR detection coming from the OS. 
2. Full stacktrace and thread information (with deadlock detection)
3. Background/Foreground ANRs

Cons:
1. Only available on Android 11 and above
2. Not possible to access device dynamic data retroactively (battery, current available memory, etc)



**Sentry ANR detection V1 was WatchDog**

ANR -> Watchdog triggered -> Collect dynamic data -> collect static data (enrich) -> Send ANR event -> Terminate Process (or not)


Sentry ANR detection V2 (AppExitInfo)

Continuously persist dynamic data to disk -> ANR
-> Terminate process -> retrieve dynamic data from disk -> collect static data -> Send ANR event (Async)



New ANR detection internals 

`activityManager.getHistoricalExitReasons()`

ApplicaationExitInfo.REASON_ANR


Use timestamp for avoiding duplicate reporting 

Add breadcrumbs and context from disk cache 

Get thread details from System trace parsing 

`public InputStream getTraceInputStream()`

SysTraceParser is a class that does this in Sentry


What's next? 

- Use watchdog together with AppExitInfo
	- can be useful if the main thread is blocked for less than 5s
	- Notifies if the user clicked "Wait" on ANR dialog and the process continued. 
	- Gives more context data 
		- Screenshots 
		- Current memory
		- Current battery
- Persist profiles across app launches
	- Know which methods were called prior to ANR












