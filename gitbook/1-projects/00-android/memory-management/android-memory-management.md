In most cases, every Android application runs in its own Linux process. This process is created for the application when some of its code needs to run and remains running until the system needs to reclaim its memory for use by other applications and it is no longer needed.

An unusual and fundamental feature of Android is that an application process's lifetime _isn't_ directly controlled by the application itself. Instead, it is determined by the system through a combination of the parts of the application that the system knows are running, how important these things are to the user, and how much overall memory is available in the system.

It is important that application developers understand how different application components (Activity, Service and Broadcast receivers) impact the lifetime of the application's process. **Not using these components correctly can result in the system killing the application's process while it is doing important work.**

----

### What is memory management in android?

Heart of android operating system 
- Linux
- Linux Kernel

Every time an app is opened, a new process is created inside linux.

Process needs resources

Resources needed:
CPU time 
I/O 
RAM


System with limited RAM

App asks linux kernel for memory for all the things it does.

Available memory 

4GB RAM 
- Linux
- Android
- Apps

Chunks of available memory 
Pages - 4KB pages 

Running out of memory 

- Swapping 
- Kill an existing process


Swapping is an idea taken from servers and operating systems. In android swapping happens via ZRAM.

Swapping means a portion of less frequently used data is put into another space (typically disk) and then read back into memory when needed.


ZRAM 

- Compressed ram 
- z - compress in unix terms 
- ZRAM swap can increase the amount of memory available in the system by compressing memory pages and putting them in a dynamically allocated swap area of memory
- Via ZRAM, instead of disk, the same memory (dedicated space for compressed data) is used.

Thrashing happens when there is a continuous reading in and writing out of swap pages in swap files. 
Android doesn't allow thrashing rather it starts KILLING! 

It picks up recently unused app and kills and frees up memory and lets the new process begin and expands memory foot print.


So app devs should consider this case of [[Process Death]] whenever writing apps. The user can background the app and the system can kill it as it likes. 


-----

### Memory Management  by Game Developer blog
[Sponsored: Tips for optimizing Android application memory usage](https://www.gamedeveloper.com/programming/sponsored-tips-for-optimizing-android-application-memory-usage)

Android uses paging and mmap instead of providing swap space which means no memory that our app touches cannot be pages out unless all the references are released. 

DVM (Dalvik VM) heap size for app process is limited. 
Starts with 2MB and goes up to "largeHeap" which can be limited to 36MB (depends on the specific device config.)
Large heap apps include Gallery, Home screen, Photo/Video Editors

Android stores background app processes in LRU cache. 

During memory crunch scenarios (low on memory), then it will kill processes according to LRU strategy, but it will also consider which app is the largest memory consumer. 

Max background process count is 20. (Depends on the specific device config.)

If we want the app to live longer even when backgrounded, we need to be a good citizen and deallocate the memory unused before being backgrounded. 

----

### Tips

For building scalable and stable mobile apps, we need to be concerned about the memory usage of our apps. 

1. Avoid using abstractions concept unnecessarily
2. Avoid using enums as it will cause double memory allocation. Use ordinary static constants. 
3. Prefer optimized SparseArray-like containers over HashMap for efficient mapping in Android development, mitigating memory overhead and performance issues associated with entry object allocation and autoboxing/unboxing. However, reserve their usage for smaller datasets, as they may exhibit slower performance for large datasets with thousands of records.
4. Minimize object creation to optimize memory usage and reduce garbage collection overhead. Avoid allocating memory for short-term temporary objects whenever possible to improve performance and efficiency
5. Before allocating memory, check the available heap of your application using ActivityManager::getMemoryClass() to avoid OutOfMemory Exceptions. If needed, consider using a 'largeHeap' declaration in AndroidManifest.xml and querying the estimated large heap size with ActivityManager::getLargeMemoryClass()
6. Coordinate with the system by implementing onTrimMemory() callback. Implement ComponentCallbacks2::onTrimMemory(int) in your Activity/Service/ContentProvider to gradually release memory according to latest system constraints. The onTrimMemory(int) helps overall system response speed, but alsokeep your process alive longer in the system.  
		When TRIM_MEMORY_UI_HIDDEN occurs, it means all the UI in your application has been hidden and you need to free UI resources. When your application is foreground, you may receive TRIM_MEMORY_RUNNING[MODERATE/LOW/CRITICAL], or in the background you may receive TRIM_MEMORY_[BACKGROUND/MODERATE/COMPLETE]. You can free non-critical resources based on the strategy to release memory when system memory is tight.
7. Exercise caution when using services, ensuring they're only kept running when actively performing tasks. Consider using IntentService to automatically finish when the task is complete, preventing system performance degradation and potential user dissatisfaction. For long-running applications like music players, split into UI and background processes with 'android:process' in AndroidManifest.xml, ensuring the background process doesn't interact with UI to prevent excessive memory allocation.
8. Exercise caution when incorporating external libraries into your Android projects, as they may not be optimized for mobile devices. Evaluate the effort required to port and optimize the library for mobile use before integration. Consider implementing specific features yourself if using only a small portion of the library's functionality to avoid unnecessary overhead.
9. Optimize bitmap usage by loading images at the appropriate resolution or scaling down higher-resolution bitmaps to match display requirements, reducing memory consumption and improving performance.
10. Use Proguard* and zipalign. The Proguard tool removes unused code and obfuscates classes, methods and fields. It will compact your code to reduce required RAM pages to be mapped. The zipalign tool will re-align your APK. More memory will be needed if zipalign not running because resource files cannot mapped from the APK.





-----
### **How to Avoid Memory Leaks** 
**How to Avoid Memory Leaks**

1. Remember to close the cursor after querying the database. If you want to keep the cursor open long-term, you must use it carefully and close it as soon as the database task finished.
2. Remember to call unregisterReceiver() after calling registerReceiver().
3. Prevent Context leakage by avoiding static member variables referencing Context objects, such as Drawables, in Activities. In cases like setting a background Drawable in onCreate(), be mindful that retaining references to Contexts can lead to memory leaks, particularly evident after screen rotation when new Activity instances are created but old ones remain due to lingering references.
	There are two ways to avoid this kind of leakage:  
  
	- Do not keep long-lived references to a context-activity. A reference to an activity should have the same life cycle as the activity itself.  
  
	- Try using the context-application instead of a context-activity.
4. Avoid non-static inner classes in an Activity. In Java, non-static anonymous classes hold an implicit reference to their enclosing class. If you're not careful, storing this reference can result in the Activity being retained when it would otherwise be eligible for garbage collection. So instead, use a static inner class and make a weak reference to the activity inside.
5. Exercise caution when using Threads in Android, as they are retained by the system and can lead to memory leaks if left running indefinitely. Instead, utilize Android's built-in concurrency mechanisms such as Loaders, Services with BroadcastReceivers, and AsyncTasks for short-lived background operations to ensure proper memory management and adherence to the Activity lifecycle
