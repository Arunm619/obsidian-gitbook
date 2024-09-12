
ANR watch dog implementation - original - [feat(android): implement ANR watchdog to track ANRs by abhaysood · Pull Request #69 · measure-sh/measure · GitHub](https://github.com/measure-sh/measure/pull/69)

ANR SigQuit is better but doesn't track background ANRs. 
Background ANR will not be detected if user chooses don't show bg ANRs. (default is false in dev options)

Process exit reason -> works from Android 11+ 
Detects both FG and BG ANRs. 



Vibin
Hi, i'm currently evaluating Bugsnag and Sentry and one of the differences i've observed in the SDK is that Bugsnag uses a SIGQUIT signal handler to get called by OS when ANR occurs, as opposed to Sentry, which uses the watchdog approach.

I have used [https://github.com/SalomonBrys/ANR-WatchDog](https://github.com/SalomonBrys/ANR-WatchDog) in production before and while it's a useful library, I saw that it reports many false-positives compared to Play Console, especially in case of ANRs in BroadcastReceivers.

SIGQUIT approach is also not perfect, though. It doesn't track background ANRs: [bugsnag/bugsnag-android#1377](https://github.com/bugsnag/bugsnag-android/issues/1377)

There's a third approach to track ANRs and Crashlytics' Alpha version seems to be using it (tracks both foreground and background ANRs): [getHistoricalProcessExitReasons](https://developer.android.com/reference/kotlin/android/app/ActivityManager#gethistoricalprocessexitreasons) on Android 11 and above only, sadly.