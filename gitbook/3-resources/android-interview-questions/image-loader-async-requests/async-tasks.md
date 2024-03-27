
Sure, we can use Android's built-in threading mechanisms, such as `AsyncTask` or `HandlerThread`, to handle the asynchronous operations. However, please note that these mechanisms are considered to be outdated and less efficient compared to modern solutions like Coroutines or RxJava. 

Here's how you can modify the `ImageLoader` class to use `AsyncTask`:

```kotlin
import android.os.AsyncTask
import java.lang.ref.WeakReference

class ImageLoader {
    private val activeTasks = mutableMapOf<Request, ImageLoadTask>()

    fun load(request: Request) {
        val imageViewRef = WeakReference(request.imageView)
        val task = ImageLoadTask(request, imageViewRef, this)
        activeTasks[request] = task
        task.execute()
    }

    fun cancelRequest(request: Request) {
        activeTasks[request]?.cancel(true)
        activeTasks.remove(request)
    }

    fun cancelAll() {
        for (task in activeTasks.values) {
            task.cancel(true)
        }
        activeTasks.clear()
    }

    internal fun onTaskCompleted(request: Request) {
        activeTasks.remove(request)
    }
}

private class ImageLoadTask(
    private val request: Request,
    private val imageViewRef: WeakReference<ImageView>,
    private val loader: ImageLoader
) : AsyncTask<Void, Void, Bitmap>() {

    override fun doInBackground(vararg params: Void?): Bitmap {
        return loader.downloadBitmap(request)
    }

    override fun onPostExecute(result: Bitmap) {
        imageViewRef.get()?.setImageBitmap(result)
        loader.onTaskCompleted(request)
    }
}
```

In this code, `ImageLoadTask` is an `AsyncTask` that downloads the bitmap in the background and sets it to the `ImageView` in the UI thread when the download is complete. The `ImageLoader` class keeps track of the active tasks and provides methods to cancel them.

Please note that `AsyncTask` was deprecated in API level 30. It's recommended to use the `java.util.concurrent` package or `Kotlin Coroutines` for new projects.