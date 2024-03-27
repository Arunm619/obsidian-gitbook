
In Android, the memory heap refers to the runtime data area from which memory for all class instances and arrays is allocated. The heap is created when the JVM starts up and may increase or decrease in size while the application runs. 

When the heap becomes full, garbage is collected. During the garbage collection, objects that are no longer used are cleared, thus making space for new objects. 

The size of the heap can vary across different devices based on the memory the device has available. Android has a limit on the heap size for each app to ensure that an app doesn't use up all the device's memory. This limit varies by device and can be queried programmatically using the `getMemoryClass()` method of the `ActivityManager` class.

Here's an example of how you might use this method in an Android app:

```kotlin
val activityManager = getSystemService(Context.ACTIVITY_SERVICE) as ActivityManager
val memoryClass = activityManager.memoryClass
Log.d("MemoryInfo", "Heap limit (MB): $memoryClass")
```

In this example, `memoryClass` is the maximum available heap size in megabytes. If your app needs to allocate large objects and you're concerned about the heap size limit, you can use the `getLargeMemoryClass()` method instead, which returns the maximum heap size if your app is running in a large heap environment.

Remember, even though you can query and monitor the heap size, the actual memory management is handled by the Android Runtime (ART) or Dalvik. You don't typically need to interact with the heap directly in your code. Instead, you should focus on writing efficient code that minimizes unnecessary object creation and avoids memory leaks.

----
High level pointers on heap

In Android, the memory heap is the region of memory used for dynamic memory allocation. It's where objects are allocated and deallocated during the runtime of an application. The heap is managed by the Android Runtime (ART) or Dalvik, depending on the version of Android.

Here are some key points about the memory heap in Android:

1. **Heap Size**: The size of the heap can vary across different devices based on the memory the device has available. Android has a limit on the heap size for each app to ensure that an app doesn't use up all the device's memory. This limit varies by device and can be queried programmatically using the `getMemoryClass()` method of the `ActivityManager` class.

2. **Garbage Collection**: When the heap becomes full, garbage is collected. During the garbage collection, objects that are no longer used are cleared, thus making space for new objects. The garbage collector is a part of the Android Runtime that automatically reclaims memory from objects that are no longer in use.

3. **Memory Allocation and Deallocation**: When an object is created in your code, memory is allocated on the heap. When the object is no longer needed, the garbage collector deallocates (frees) the memory, making it available for future allocations.

4. **OutOfMemoryError**: If the heap is full and there's not enough memory to allocate for a new object, an OutOfMemoryError is thrown.

5. **Heap Dumps**: A heap dump is a snapshot of the memory of a Java process. The heap dump contains information about the Java objects and classes in the heap at the moment the snapshot is triggered. It's mainly used for debugging memory issues such as memory leaks and high memory consumption.

Remember, while you can monitor the heap size and garbage collection in Android, the actual memory management is handled by the Android Runtime. You don't typically need to interact with the heap directly in your code. Instead, you should focus on writing efficient code that minimizes unnecessary object creation and avoids memory leaks.