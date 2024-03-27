Py - Pierre - Originally from France


Leak Canary - Memory Leak detection 
Helps fix OOM errors and ANRs.

 Dagger 
 Retrofit 
 OkHttp

Logcat - [GitHub - square/logcat: I CAN HAZ LOGZ?](https://github.com/square/logcat) Memory efficient logs (better than timber)
Curtains - [GitHub - square/curtains: Lift the curtain on Android Windows!](https://github.com/square/curtains)  Window management in android
PAPA - Perf of android prod apps
Annotation Processing Library - First annotation processor for android in java

Performance on Android doc has very little info and has nuances for different use cases.
- No content
- No training

ANR - Blocking Main thread in theory But in real life, its not that straightforward.
`While learning something new, write it down so it can teach others.`

Learnings:
1. Start with perfetto - birds eye view
2. Profiler - Flame Chart - see whats taking tim
3. Use a prod build - Not debug builds 
4. Use specific flags


---
Kirk Pipidrine - Java performance expert - Investigating perf issues 

first instinct / thing to do: jump to code. DONT DO THAT. 
Do outside in. Figure out the shape of the problem. Birds eye view. 
General location of the problem and progressively zoom in. 

Once you understand the problem, then go fix exactly where it is. 


Macro benchmark uses perfetto under the hood. 
Perfetto usage : Add multiple Trace sections 



Trace.beginSection and Trace.EndSection 

creates bands - color blocks 

Android framework add few bands - Choreographer and Layout 

Giant hack - main thread loop - every message - runnable - tostring - duration in perfetto 

We can know whats happening exactly when we look at the perffetto 
1. executors - Background 
2. coroutines 


Profilers - 2 family
1. Perfetto is tracing - based on spans (bands) - liteweight
2. Sampling profiler - In android studio - two issues - takes stack traces in between  - so somethings may go missing in between stack dumps - impacts run time 

perf investigations are fun - mystery 

Profile the changes when raising PR 
because perf issues can slip thru the cracks

Whenever you are seeing a jank/ issue with the app performance, dont move on quoting "its a debug app thing"


Meetups 
Android Study Group - Slack 
Kotlin Slack 


---

Mobile is a fun-engineering 
Backend is a serious engineering 

----
French!

Problem solving is the real passion for coding. 
Software engineering leads to system thinking. 
System thinking can be applied to everything in life. 


---
Team = Manager + peers = drives the perception of the entire company


From: Open source code Android
To: UX, product, business, teams, organisation 






 

