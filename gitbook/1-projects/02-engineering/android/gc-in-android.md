
Android uses a garbage collector for automatic memory management. The garbage collector in Android is known as Dalvik/ART Garbage Collector. 

The garbage collector's role is to find data objects in a program that cannot be accessed in the future and reclaim the resources (memory) used by those objects. It works by tracking each and every allocation of memory and determining if it is still needed. If memory is not needed, the garbage collector reclaims it.

In Android, garbage collection has evolved over the years:

1. **Dalvik GC**: In the early versions of Android, the Dalvik runtime was used, which had a mark-sweep garbage collector. It was a stop-the-world garbage collector, meaning it stopped the application from running while it was collecting garbage, which could lead to performance issues.

2. **Concurrent Mark Sweep (CMS) GC**: In Android 3.0 (Honeycomb), the garbage collector was improved to include a concurrent garbage collector. This meant that the garbage collector could run in the background while the application was running, reducing pauses due to garbage collection.

3. **ART GC**: In Android 5.0 (Lollipop), the Android runtime (ART) was introduced, which uses a combination of mark-sweep and mark-compact garbage collection. The mark-compact collector compacts the remaining objects to the bottom of the heap after the garbage is collected, reducing memory fragmentation.

4. **Incremental GC**: In Android 7.0 (Nougat), incremental garbage collection was introduced, which further reduces pauses due to garbage collection by breaking the garbage collection process into smaller parts and running each part incrementally.

5. **Concurrent copying GC**: In Android 8.0 (Oreo), a concurrent copying garbage collector was introduced for the old generation of objects, reducing pauses due to garbage collection.

Remember, while the garbage collector helps manage memory, it's still important to write efficient code and manage resources properly to ensure the best performance for your Android apps.