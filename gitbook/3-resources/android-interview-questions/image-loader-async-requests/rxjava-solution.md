
Asynchrony Solution

Sure, I can help you rewrite the code using RxJava. Here's a step-by-step plan:

1. We will use `Observable` to handle the asynchronous operations.
2. We will use `Schedulers.io()` to run the network requests in a separate thread.
3. We will use `flatMap` operator with a maxConcurrency parameter to limit the parallelism to 2 threads.
4. We will use a `CompositeDisposable` to keep track of the active jobs, so we can cancel them if needed.
5. We will use a `WeakReference` to hold the `ImageView` to avoid leaking it.
6. We will use a `LifecycleObserver` to auto-cancel in-flight requests when the `ImageView` is gone from the viewport.

Let's start by modifying the `ImageLoader` class:

```kotlin
import io.reactivex.Observable
import io.reactivex.disposables.CompositeDisposable
import io.reactivex.schedulers.Schedulers
import java.lang.ref.WeakReference

class ImageLoader {
    private val compositeDisposable = CompositeDisposable()

    fun load(request: Request) {
        val imageViewRef = WeakReference(request.imageView)
        val disposable = Observable.just(request)
            .subscribeOn(Schedulers.io())
            .flatMap({ r ->
                Observable.just(downloadBitmap(r))
            }, false, 2)
            .subscribe({ bitmap ->
                imageViewRef.get()?.setImageBitmap(bitmap)
            }, { error ->
                println("Download failed for $request")
            })

        compositeDisposable.add(disposable)
    }

    fun cancelRequest(request: Request) {
        compositeDisposable.clear()
    }

    fun cancelAll() {
        compositeDisposable.clear()
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



---

The `.flatMap` operator is used in RxJava to transform the items emitted by an Observable into Observables, then flatten the emissions from those into a single Observable.

In the code snippet you provided,

```.flatMap({ r -> Observable.just(downloadBitmap(r)) }, false, 2)```

 the `flatMap` operator is used to transform each `Request` object `r` into an `Observable` that emits the result of `downloadBitmap(r)`.

The `false` argument is for the `delayError` parameter. When it's set to `false`, if one of the transformed Observables fails, the resulting Observable immediately issues an error notification and stops emitting items. If it's set to `true`, all transformed Observables are allowed to complete before the error notification is issued.

The `2` argument is for the `maxConcurrency` parameter. It limits the number of concurrent subscriptions created when transforming the source items into Observables. In this case, it means that a maximum of 2 concurrent network requests can be made.