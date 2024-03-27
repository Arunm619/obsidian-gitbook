
- We are sharing drive link with the folks 


Asynchrony assignment - [AsynchronyAssignment.zip - Google Drive](https://drive.google.com/file/d/1Z0ppA1XoDd-Thyr5G7me8XGQ9fA3owOb/view)
Live data assignment - [LiveDataAssignment.zip - Google Drive](https://drive.google.com/file/d/1Xk_UEf-F8iWBmJGsM3A7oW33OwH6CLTr/view)



Asynchrony Solution

1. We will use Kotlin Coroutines to handle the asynchronous operations.
2. We will use a `Dispatchers.IO` dispatcher to run the network requests in a separate thread.
3. We will use a `Semaphore` to limit the parallelism to 2 threads.
4. We will use a `MutableMap` to keep track of the active jobs, so we can cancel them if needed.
5. We will use a `WeakReference` to hold the `ImageView` to avoid leaking it.
6. We will use a `LifecycleObserver` to auto-cancel in-flight requests when the `ImageView` is gone from the viewport.

Let's start by modifying the `ImageLoader` class:

```kotlin
import kotlinx.coroutines.*
import java.lang.ref.WeakReference
import java.util.concurrent.Semaphore
import kotlin.coroutines.CoroutineContext

class ImageLoader : CoroutineScope {
    private val job = Job()
    private val semaphore = Semaphore(2)
    private val activeJobs = mutableMapOf<Request, Job>()
    override val coroutineContext: CoroutineContext
        get() = Dispatchers.IO + job

    fun load(request: Request) {
        val imageViewRef = WeakReference(request.imageView)
        val job = launch {
            semaphore.acquire()
            try {
                val bitmapStream = downloadBitmap(request)
                val bitmap = decodeBitmap(bitmapStream)
                withContext(Dispatchers.Main) {
                    imageViewRef.get()?.setImageBitmap(bitmap)
                }
            } catch (e: IOException) {
                println("Download failed for $request")
            } finally {
                semaphore.release()
                activeJobs.remove(request)
            }
        }
        activeJobs[request] = job
    }

    fun cancelRequest(request: Request) {
        activeJobs[request]?.cancel()
        activeJobs.remove(request)
    }

    fun cancelAll() {
        job.cancel()
    }
}
```

Next, let's modify the `ImageView` class to implement `LifecycleObserver`:

```kotlin
import androidx.lifecycle.Lifecycle
import androidx.lifecycle.LifecycleObserver
import androidx.lifecycle.OnLifecycleEvent

class ImageView : LifecycleObserver {
    private var bitmap: Bitmap? = null

    fun setImageBitmap(bitmap: Bitmap) {
        this.bitmap = bitmap
        println("Bitmap $bitmap set at ${currentTimeMillis()} for ImageView $this")
    }

    @OnLifecycleEvent(Lifecycle.Event.ON_DESTROY)
    fun onDestroy() {
        ImageLoader().cancelAll()
    }
}
```

Finally, you need to add the `ImageView` as an observer to the lifecycle of the activity or fragment that contains it:

```kotlin
lifecycle.addObserver(imageView)
```

Please note that this code assumes that you are using Android's `Lifecycle` library. If you are not, you will need to manually call `ImageLoader().cancelAll()` when the `ImageView` is gone from the viewport.