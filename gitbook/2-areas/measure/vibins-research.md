

[Consider using a more accurate ANR tracking implementation · Issue #1796 · getsentry/sentry-java · GitHub](https://github.com/getsentry/sentry-java/issues/1796)

Hi, i'm currently evaluating Bugsnag and Sentry and one of the differences i've observed in the SDK is that Bugsnag uses a SIGQUIT signal handler to get called by OS when ANR occurs, as opposed to Sentry, which uses the watchdog approach.

I have used [https://github.com/SalomonBrys/ANR-WatchDog](https://github.com/SalomonBrys/ANR-WatchDog) in production before and while it's a useful library, I saw that it reports many false-positives compared to Play Console, especially in case of ANRs in BroadcastReceivers.

SIGQUIT approach is also not perfect, though. It doesn't track background ANRs: [bugsnag/bugsnag-android#1377](https://github.com/bugsnag/bugsnag-android/issues/1377)

There's a third approach to track ANRs and Crashlytics' Alpha version seems to be using it (tracks both foreground and background ANRs): [getHistoricalProcessExitReasons](https://developer.android.com/reference/kotlin/android/app/ActivityManager#gethistoricalprocessexitreasons) on Android 11 and above only, sadly.


-----------


[Background ANRs are not tracked · Issue #1377 · bugsnag/bugsnag-android · GitHub](https://github.com/bugsnag/bugsnag-android/issues/1377)


The SIGQUIT-based ANR tracker that's present in the library doesn't track ANRs that happen in background if user has "Show background ANRs" switched off (which is the default value) in Developer options.

Any workaround for this?

Logs when the ANR occurs (without any dialog):

```
Thread[4,tid=14199,WaitingInMainSignalCatcherLoop,Thread*=0x712fa7be90,peer=0x12c40cd8,"Signal Catcher"]: reacting to signal 3
I  Wrote stack traces to tombstoned

Process com.my.package (PID: 14189) ended
```


----
App Exit Info can be used to identify better data
