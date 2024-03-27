[What's new in Android vitals: A deep dive into Play's technical quality bar - YouTube](https://www.youtube.com/watch?v=HvHYXTO-_-Y&t=1s&pp=ygUTcGxheSBjb25zb2xlIHZpdGFscw%3D%3D)

Achieving Play's technical quality bar

Everyone's favourite topic ANR.

| Metric                     | Overall Quality | Per-Phone Quality |
|----------------------------|-----------------|-------------------|
| User-perceived Crash Rate |     1.09%       |        8%         |
| User-perceived ANR Rate   |     0.47%       |        8%         |

Overall quality limit breach means lower visibility on all devices. 

Per-Phone Quality limit breach means On those phones A warning may be displayed on store listing. 


---
**Debug guidance** 
Suggestions and extra information to make debugging easier. 

**Suggested fixes***
Guidance on how to fix the problem

---

Android Vitals - Overview 

Core vitals 
1. User perceived ANRs
2. User perceived Crashes

Also, list of Crashes + ANRs

Crash or ANR details 

Stack Traces, Thread dumps 

Various details like Android version, device type are there for drilling down the details. 

---
**Platform issues causing crashes***

Issues caused by compatibility problems with Play platforms such as Google Play Games on Widnows or Play as you Download, are indicated. 

While rare, this allows you to focus on issues you can fix, while the platform teams can focus on platform issues. 


----
- Debugging help in ANR 
- Common cause of ANR and fixes

**Unactionable ANRs***

Sometimes the Android OS captures the ANR thread dump too late to see the actual problem. 

We highlight these ANRs for you so don't spend unnecessary time on them. 

We recommend you focus on actionable ANRs which are likely to be related. 


Insight called `Main Thread Idle` has been created for issues for which the thread dump with the problem hasn't been captured. 

Not capturing what is called as `Guilty thread dump`
is non-deterministic. ANRs are a bit squirrely and sometimes the thread dump shows a guilty code and sometimes it doesn't.

When the ANR thread dump shows as Main thread idle, the actual reason for ANR could be many different things.

---
Imagine a scenario where an app has 5 different errors that lead to ANRs. 

Sometimes the OS detects the guilty thread dump and sometimes it captures the normal operation. 

When captures the guilty thread, Vitals will group into One of the Five ANRS in your issues list corresponding to the five underlying issues. 

When the OS detects the normal operation, it detects into a sixth main thread idle ANR. 

This is because parts of ANR thread dumps are used for grouping. 

Because there are 5 different underlying ANRs that are feeding into this sixth ANR with main thread idle, the main thread idle ANR will often the biggest in the list. 

----
```caution
Ignore ANRs with 'Main Thread Idle' Insight, Instead focus on fixing ANRs with useful thread dumps.

```

----
**Native Memory Errors**

Memory errors are both bad for users and security errors. 

Major type of Memory Error is `Used After Free Error`

GWP-ASan ensures your game consistently crashes when it illegally accesses memory.

Makes it easier to pinpoint use-after-free and heap-buffer-overflow errors.

Enable it with a single-line manifest change, and see the extra stack trace in Vitals.

When a memory location is used after freeing it can do different things
- Can behave weirdly
- Can crash
- App can do something funny if the memory contents have changed but the memory isn't reserved by the process that did the changing.
- Or the app can keep running fine with contents as they were left.

This inconsistency makes it hard to track down and to fix these issues. 

GWP-AS force crashes the app when it does an illegal memory access.

It only does a small fraction of the time so it minimally affects your crash rate.

GWP-AS adds bread crumbs for the memory allocation and deallocation for the illegal memory state and gets extra info about the thread dumps for more insights.

```xml
 android:gwpAsanMode="always"
```
Goes into the manifest.xml and android does the rest. 

GWP-ASan is a native memory allocator feature that helps find [use-after-free](https://cwe.mitre.org/data/definitions/416.html) and [heap-buffer-overflow](https://cwe.mitre.org/data/definitions/122.html) bugs. Its informal name is a recursive acronym,"**G**WP-ASan **W**ill **P**rovide **A**llocation **SAN**ity"

---
**SDK Notes**

Suggested fixes for your SDK-related issues, provided by SDK developers.

Play has a product called `SDK console`
where SDK developers can register their SDK and learn about crashes that are caused by their SDK. 

With SDK notes, SDK developers can provide suggestions for how to fix crashes that are caused by their SDKs. 

These are potential fixes for the crashes provided by the SDK developers themselves. 

Details page of the crash will surface the SDK note if the SDK developer has provided that info.

Not all crashes will have that info. 
We can also submit the crashes as they occur to the SDK owners for investigating the issues.

----
**How to fix crashes**

**PendingIntent Mutability***

In nov 22, Target SDK was set to API 31 for app updates. 

Many apps updated the target SDK but didn't make the necessary code changes to support the target level API. 
Specifically apps needs to specify the mutability of each pending intent. 

If not specified app will crash on Android 12 or above. 

This is one of the major issues in android right now. 

Vital consoles will now surface this issue's fix when your app is facing this problem.

----
Summary
- Debug Guidance 
	- Platform issue flagging 
	- ANR Actionability
	- GWP-ASan for native memory errors
- Suggested Fixes
	- SDK Notes
	- PendingIntent Mutability
---
**Android Vitals 

**James Heather Engineering Manager** 

For Power Users, Android Vitals API is provided. We can use the API for creating internal dashboards. 

Eg. Gameloft has successfully integrated the APIs to enhance their internal dashboards and bring all their KPIs into one place to help teams move faster. 


---
Android Vitals API - hourly data

From daily we have now daily data in the API only.
- Hourly data
	- Detect issues faster
	- Catch release or server side issues
- Caveat
	- Need to understand app's daily fluctuations based on usage patterns


---

**ANR deep dive**

- Common types of ANR
- How to fix them 

ANR occurs when the main thread AKA UI thread of the android app is blocked for too long. 

To a user, it looks and feels like the app/game is frozen.

Sometimes ANR gets resolved on its own. Sometimes the OS kills the app/game. And sometimes the user manually kills the game and hopefully reopens it.

All android developers need to be familiar with ANRs:

They affect all apps and games and can be tricky to track down and especially to reproduce as they can be affected by the state of the system overall.

Fixing ANRs can increase engagement and revenue by ensuring users can use the app as it was designed to be.


OkCredit 
- reduced ANR by 60%
- Improved day 1 customer retention of low-end devices by about 22%
- Improved app rating from 4.3 to 4.6 on the playstore
- Cold startup time improved by ~70%
- Saw 60% improvement in user click to full draw of first frame on any screen

----
Insights : How Vitals will show debug guidance

Insight title 
Insight message
Stack trace annotations
Issues list indicators

---
Common Cause of ANR #1

Main thread busy doing binder calls. 

Binder is android's IPC (inter process communication mechanism). Binder can be expensive and the duration can be unpredictable.

The main thready was busy doing a binder call that was potentially slow. 

What to do:

- You should avoid as much as possible making binder calls in the main thread, although sometimes this is unavoidable.
- Make sure to instrument and monitor such calls to detect slowness.

UI Treatment:
- Highlight the slow binder call
- Highlight where your code starts the slow binder call.

```
This binder call is slow on line #x
This is where you start the binder call which is slow on line #Y
```

---

Common Cause of ANR #2

Doing I/O on the Main Thread

The main thread was busy performing an I/O Operation. This could be network or file access (especially compressed files.)
But it can also be a seemingly innocuous operation such as `ClassLoader.loadClass`.


What to do:

- I/O Operations are very unpredictable and can block a thread for a long time. Please avoid IO in the main thread at all costs as it is very unpredictable.
- Refactor all your code so that I/O Operations are done in a separate thread from the main thread. 
UI Treatment: 
- Highlight where the I/O operation is

```
This function call is performing I/O which has very unpredictable timing. It should be moved out of the main thread.
```
----

Common Cause of ANR #3 

 Main thread blocked
The main thread is blocked trying to acquire a lock that's held by another thread. 

What to do: 
- Try to minimise the use of locks in the main thread, and make sure that whoever holds those locks doesn't hold them for long. 
- Avoid expensive and unpredictable operations like I/O or Binder calls while holding a lock.
UI treatment:
- Highlight where main thread is trying to acquire the lock
- Highlight which thread is holding the lock and where

```
The main thread is blocked here. It is waiting on lock <x> (a java.util.HashMap) which is held by thread #Y.

This thread is blocking the main thread, as it holding the lock here. <x> (a java.util.HashMap)

```

----

Common Cause of ANR #4 

Main Thread Busy on Native Lock

The main thread is blocked, waiting on a native synchronisation routine such as a mutex.

What to do:
- Native synchronization routines don't provide details on the exact lock or where it is being held. 
- Find the locked mutext in your source, and then locate other code locations where it is being acquired. You can use Android Studio's profiler to detect potential lock contention if multiple threads frequently compete for the same lock. 
UI Treatment:
- Highlight where the main thread is waiting. 

```
The native synchronization routine is blocking the main thread causing an ANR.
```


----

**Common ANR situtation***

These issues are not actionable as the stack traces do not show the blocking condition that is causing the ANR. This type of ANRs reports are produced when the android platform is unable to capture the ANR stack trace in a timely manner, and the ANR condition has passed by the time the stack trace is captured. This is usually caused by high load or resource contention inside the android system server which may in turn contribute to the root cause of the ANR.


What to do:
- It is impossible to determine the root cause of ANRs where the main thread is idle. 
- These ANRs are included in Android Vitals for completeness as they allow you to be aware of the true numbers of users affected by ANRs. In general, to fix the issue underlying root cause, you should look at ANRs with the same type and activity, but with different main thread states. 

UI Treatment:
- Message in the stack trace explaining that the ANR reason isn't captured. 

```
Your app encountered an ANR, but the stack trace captured doesn't show the problem.
```


-----









