
com.meesho.discovery.api.product.ProductReviewJsonAdapter.fromJson

Link - [Google Play Console](https://play.google.com/console/u/0/developers/8586507075174719506/app/4974541337588252131/vitals/crashes/3523a9c6d3539bc7765f06c23b56720c/details?days=28&isUserPerceived=true)


| Category       | Count | Period         |
| -------------- | ----- | -------------- |
| Affected users | 10.2K | Last 28 days   |
| Events         | 10.5K | Last 28 days   |
| Last occurred  | -     | 2 hours ago    |
| Last updated   | -     | Today, 2:30 PM |

Insights
The main thread was blocked trying to acquire a lock that was held by another thread


Main thread was blocked because another thread was it was waiting for a lock acquired by another candidate.

```plain
The main thread is blocked here. It is waiting, trying to acquire lock **0x00ba4f87 (ck.q)**, held by thread 157. [Learn more](https://developer.android.com/topic/performance/anrs/find-unresponsive-thread#lock-contention)


Lock **0x00ba4f87 (ck.q)**, was acquired by this thread here. This is causing an ANR, as the main thread is blocked trying to acquire the same lock. 
```

Lock was acquired by ```

```java
at com.squareup.moshi.adapters.Rfc3339DateJsonAdapter.fromJson (Rfc3339DateJsonAdapter.java:41)
```



Issue code:

```kotlin
 private fun writeToPrefs(event: AppSessionEvent) {
        prefs.edit().putString(PrefConstants.APP_SESSION_EVENT, moshiUtil.toJson(event)).apply()
    }
```


Fix code:
```kotlin
private fun writeToPrefs(event: AppSessionEvent) {
        disposable =
            Completable.fromAction {
                    val appSessionEventData = moshiUtil.toJson(event)
                    prefs
                        .edit()
                        .putString(PrefConstants.APP_SESSION_EVENT, appSessionEventData)
                        .apply()
                }
                .subscribeOn(schedulerProvider.io())
                .subscribe({}, Timber::e)
    }
```


Moved the heavy work of Json String Conversion off the main thread. 

PR -  [# DNC-6462 ANR: Main thread blocked](https://github.com/Meesho/supply_android/pull/8105)
