
 com.meesho.supply.analytics.db.ViewedHighVizFiltersDao_Impl$3.call
 
 **android.database.sqlite.SQLiteReadOnlyDatabaseException***

ANR Link - [Google Play Console](https://play.google.com/console/u/0/developers/8586507075174719506/app/4974541337588252131/vitals/crashes/a9c4cd57072594f4a8fd52542710534c/details?days=28&isUserPerceived=true)


#### Stack Trace

```kotlin
Exception io.reactivex.exceptions.OnErrorNotImplementedException: The exception was not handled due to missing onError handler in the subscribe() method call. Further reading: https://github.com/ReactiveX/RxJava/wiki/Error-Handling | android.database.sqlite.SQLiteReadOnlyDatabaseException: attempt to write a readonly database (code 1032 SQLITE_READONLY_DBMOVED)
  at io.reactivex.internal.observers.EmptyCompletableObserver.onError (EmptyCompletableObserver.java:50)
  at io.reactivex.internal.operators.observable.ObservableFlatMapCompletableCompletable$FlatMapCompletableMainObserver.onError (ObservableFlatMapCompletableCompletable.java:126)
  at io.reactivex.internal.operators.observable.ObservableFlatMapCompletableCompletable$FlatMapCompletableMainObserver.innerError (ObservableFlatMapCompletableCompletable.java:165)
  at io.reactivex.internal.operators.observable.ObservableFlatMapCompletableCompletable$FlatMapCompletableMainObserver$InnerObserver.onError (ObservableFlatMapCompletableCompletable.java:183)
  at io.reactivex.internal.operators.single.SingleFlatMapCompletable$FlatMapCompletableObserver.onError (SingleFlatMapCompletable.java)
  at io.reactivex.internal.operators.single.SingleDoOnSuccess$DoOnSuccess.onError (SingleDoOnSuccess.java:65)
  at io.reactivex.internal.operators.single.SingleDelayWithCompletable$OtherObserver.onError (SingleDelayWithCompletable.java:64)
  at io.reactivex.internal.operators.completable.CompletableFromCallable.subscribeActual (CompletableFromCallable.java:40)
  at io.reactivex.Completable.subscribe (Completable.java:2309)
  at io.reactivex.internal.operators.single.SingleDelayWithCompletable.subscribeActual (SingleDelayWithCompletable.java:36)
  at io.reactivex.Single.subscribe (Single.java:3603)
  at io.reactivex.internal.operators.single.SingleDoOnSuccess.subscribeActual (SingleDoOnSuccess.java:35)
  at io.reactivex.Single.subscribe (Single.java:3603)
  at io.reactivex.internal.operators.single.SingleFlatMapCompletable.subscribeActual (SingleFlatMapCompletable.java:44)
  at io.reactivex.Completable.subscribe (Completable.java:2309)
  at io.reactivex.internal.operators.observable.ObservableFlatMapCompletableCompletable$FlatMapCompletableMainObserver.onNext (ObservableFlatMapCompletableCompletable.java:110)
  at io.reactivex.internal.operators.observable.ObservableObserveOn$ObserveOnObserver.drainNormal (ObservableObserveOn.java:201)
  at io.reactivex.internal.operators.observable.ObservableObserveOn$ObserveOnObserver.run (ObservableObserveOn.java:255)
  at io.reactivex.internal.schedulers.ScheduledRunnable.run (ScheduledRunnable.java:66)
  at io.reactivex.internal.schedulers.ScheduledRunnable.call (ScheduledRunnable.java)
  at java.util.concurrent.FutureTask.run (FutureTask.java:266)
  at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run (ScheduledThreadPoolExecutor.java:301)
  at java.util.concurrent.ThreadPoolExecutor.runWorker (ThreadPoolExecutor.java:1167)
  at java.util.concurrent.ThreadPoolExecutor$Worker.run (ThreadPoolExecutor.java:641)
  at java.lang.Thread.run (Thread.java:920)
Caused by android.database.sqlite.SQLiteReadOnlyDatabaseException: attempt to write a readonly database (code 1032 SQLITE_READONLY_DBMOVED)
  at android.database.sqlite.SQLiteConnection.nativeExecuteForLastInsertedRowId
  at android.database.sqlite.SQLiteConnection.executeForLastInsertedRowId (SQLiteConnection.java:940)
  at android.database.sqlite.SQLiteSession.executeForLastInsertedRowId (SQLiteSession.java:790)
  at android.database.sqlite.SQLiteStatement.executeInsert (SQLiteStatement.java:89)
  at androidx.sqlite.db.framework.FrameworkSQLiteStatement.executeInsert (FrameworkSQLiteStatement.java)
  at androidx.room.EntityInsertionAdapter.insert (EntityInsertionAdapter.java:97)
  at com.meesho.supply.analytics.db.ViewedHighVizFiltersDao_Impl$3.call (ViewedHighVizFiltersDao_Impl.java:92)
  at com.meesho.supply.analytics.db.ViewedHighVizFiltersDao_Impl$3.call (ViewedHighVizFiltersDao_Impl.java:87)
  at io.reactivex.internal.operators.completable.CompletableFromCallable.subscribeActual (CompletableFromCallable.java:36)
```


#### Insights
```Insights

Provided by

Android vitals

Problem

This crash may be related to an SDK

Recommendation

You shared this crash with androidx.room:room-runtime (androidx.room:room-runtime) on Mar 11, 2024
```



#### **Occurrence details**

| Metric         | Amount | Last 28 days     |
| -------------- | ------ | ---------------- |
| Affected users | 11.3K  |                  |
| Events         |        | 11.9K            |
| Last occurred  |        | 112 minutes ago  |
| Last updated   |        | Monday, 10:30 PM |
|                |        |                  |


----

**Error Summary:**

- **Unhandled Exception:** An exception occurred but wasn't handled properly, leading to unexpected behavior and likely the ANR (Application Not Responding).
- **Root Cause:** SQLiteReadOnlyDatabaseException (code 1032 SQLITE_READONLY_DBMOVED), indicating an attempt to write to a read-only database.

**Potential Causes:**

- **Database Inaccessible:** The database file might be corrupt, locked by another process, or located on read-only storage.
- **File System Permissions:** The app might lack write permissions for the database file or its directory.
- **Room Initialization Issue:** The Room database might not have been initialized correctly or opened with write access.
- **Thread Interference:** Concurrent database operations from multiple threads without proper synchronization could cause conflicts.



**Location of Error**:

- The error originates from a call within the database interaction code, specifically during an attempt to execute an insert operation (`executeInsert`).
- It seems to be happening within the implementation of a Room DAO (`ViewedHighVizFiltersDao_Impl`), which is likely responsible for interacting with your SQLite database using Room Persistence Library.



Issue in the code:

```kotlin
disposable = (highVizImpressionTracker.trackViewableHighVizFilters().subscribe())
```

Error code - SQLITE_READONLY_DBMOVED => "Database cannot be modified because database file has moved",

[cs.android.com/android/platform/superproject/main/+/main:external/rust/crates/libsqlite3-sys/src/error.rs;l=285?q=SQLITE\_READONLY\_DBMOVED&ss=android%2Fplatform%2Fsuperproject%2Fmain&start=41](https://cs.android.com/android/platform/superproject/main/+/main:external/rust/crates/libsqlite3-sys/src/error.rs;l=285?q=SQLITE_READONLY_DBMOVED&ss=android%2Fplatform%2Fsuperproject%2Fmain&start=41)



Fix :

```
disposable = (highVizImpressionTracker.trackViewableHighVizFilters().subscribe({},{  
    Timber.e("Error in tracking high viz filters: $it")  
}))
```

Implementing the onError callback should catch the issue gracefully.