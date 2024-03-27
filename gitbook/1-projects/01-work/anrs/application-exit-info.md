

- Use system API to retrieve ANRs on next app launch

**Pros**
- Most accurate ANR detection coming from the OS
- Full stacktrace and thread information (with deadlock detection)
- Background / Foreground ANRs
**Cons**
- Only available on Android 11 and above.
- Not possible to access device dynamic data retroactively (battery, current memory, etc.)

**Implementation Detail**

The provided Kotlin code defines a class `AppExitInfoManager` that is used to manage and fetch the last exit reason of an application. This class is annotated with `@Singleton`, indicating that only a single instance of this class should exist.

The class is injected with two dependencies: a `Context` and a `SharedPreferences` instance. The `Context` is annotated with `@ApplicationContext`, meaning that it's the context of the application, not of a specific activity.

```kotlin
@Singleton
class AppExitInfoManager
@Inject
constructor(@ApplicationContext val context: Context, private val prefs: SharedPreferences) {
```

The class has a companion object that defines a constant `PREV_DETECT_TIME_KEY`. This key is used to store and retrieve the timestamp of the last exit reason from `SharedPreferences`.

```kotlin
companion object {
    private const val PREV_DETECT_TIME_KEY = "PREV_DETECT_TIME_KEY"
}
```

The `fetchLastExitReason` function is the core of this class. It fetches the last exit reason of the application. This function is annotated with `@RequiresApi(Build.VERSION_CODES.R)`, meaning it requires Android API level 30 or higher to run.

```kotlin
@RequiresApi(Build.VERSION_CODES.R)
fun fetchLastExitReason() {
```

Inside this function, it first gets the `ActivityManager` system service and retrieves the last five exit reasons of the application. It then iterates over these exit reasons and adds any unprocessed ones (those with a timestamp greater than the last stored timestamp) to a list. If it encounters an exit reason due to an Application Not Responding (ANR) error, it breaks the loop.

```kotlin
val activityManager =
    context.getSystemService(Context.ACTIVITY_SERVICE) as ActivityManager
val applicationExitInfos =
    activityManager.getHistoricalProcessExitReasons(context.packageName, 0, 5)
```

After the loop, if there are any unprocessed exit reasons, it updates the stored timestamp in `SharedPreferences` to the timestamp of the most recent unprocessed exit reason.

```kotlin
if (unprocessedExitInfos.size > 0) {
    prefs
        .edit()
        .putLong(PREV_DETECT_TIME_KEY, unprocessedExitInfos[0].timestamp)
        .apply()
}
```

Finally, it sets `lastStoredAppExitInfo` to the ANR exit reason if one was found, or to the first unprocessed exit reason otherwise.

```kotlin
lastStoredAppExitInfo =
    if (anrAppExitInfoIndex != CoreApiConstants.INT_DOES_NOT_EXIST) {
        unprocessedExitInfos[anrAppExitInfoIndex]
    } else {
        unprocessedExitInfos.firstOrNull()
    }
```

The function is wrapped in a try-catch block to handle any exceptions that might occur, logging them using the Timber library.