
[**android:largeHeap="true"**(https://developer.android.com/guide/topics/manifest/application-element#largeHeap)

**It's not a good idea to use** `android:largeHeap="true"` here's the extract from google that explains it,

> However, the ability to request a large heap is intended only for a small set of apps that can justify the need to consume more RAM (such as a large photo editing app). Never request a large heap simply because you've run out of memory and you need a quick fix—you should use it only when you know exactly where all your memory is being allocated and why it must be retained. Yet, even when you're confident your app can justify the large heap, you should avoid requesting it to whatever extent possible. Using the extra memory will increasingly be to the detriment of the overall user experience because garbage collection will take longer and system performance may be slower when task switching or performing other common operations.

here's the complete link of the documentation [https://developer.android.com/training/articles/memory.html](https://developer.android.com/training/articles/memory.html)

Here are a few **tips to deal** with `out of memory errors`

1) Use these callback that android gives **`onLowMemory`**, **`onTrimMemory(int)`** and clear the cache of image like (picasso, glide, fresco....) you can read more about them [here](https://developer.android.com/reference/android/app/Application.html) and [here](https://developer.android.com/reference/android/content/ComponentCallbacks2.html)  
2) compress your files(images, pdf)  
3) read about how to handle bitmap more efficiently [here](https://developer.android.com/topic/performance/graphics/load-bitmap.html)  
4) Use lint regularly before production pushes to ensure code is sleek and not bulky

**What You Get :**

- Obviously, you get larger heap, which means decreasing risk of `OutOfMemoryError`.

**What You Lose :**

- **You may lose some frames, which can cause a visible hitching**. Larger heap makes garbage collections take longer. Because the garbage collector basically has to traverse your entire live set of objects. Usually, garbage collection pause time is about 5ms, and you may think few milliseconds are not a big deal. But every millisecond count. Android device has to update its screen in every 16 ms and longer GC time might push your frame processing time over the 16 millisecond barrier, which can cause a visible hitching.
    
- **Also switching apps will become slower**. Android system may kill processes in the LRU cache beginning with the process least recently used, but also giving some consideration toward which processes are most memory intensive. So if you use larger heap, your process would more likely to be killed when it's backgrounded, which means it may take longer time when users want to switch from other apps to yours. Also other backgrounded processes will more likely to be kicked out when your process is foreground, because your app require larger memory. It means switching from your app to other apps also takes longer.
    

**Conclusion :**

Avoid using `largeHeap` option as much as possible. It may cost you hard-to-notice performance drop and bad user experience.

