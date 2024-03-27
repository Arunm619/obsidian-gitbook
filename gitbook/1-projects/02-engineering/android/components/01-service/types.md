Sure, let's delve into the details of the different types of Service components in Android:

1. **Started Service**: A started service is one that another component starts by calling `startService()`, which results in a call to the service's `onStartCommand()` method. Once started, a service can run in the background indefinitely, even if the component that started it is destroyed. It's typically used for tasks that should be completed but aren't directly tied to user interaction.

```kotlin
class MyStartedService : Service() {
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        // The service is starting, due to a call to startService()
        return START_STICKY
    }

    // Implement other required methods...
}
```

2. **Bound Service**: A bound service is one that allows other components to bind to it by calling `bindService()`. A bound service offers a client-server interface that allows components to interact with the service, send requests, receive results, and even do so across processes with interprocess communication (IPC).

```kotlin
class MyBoundService : Service() {
    private val binder = LocalBinder()

    inner class LocalBinder : Binder() {
        fun getService(): MyBoundService = this@MyBoundService
    }

    override fun onBind(intent: Intent): IBinder {
        return binder
    }

    // Implement other required methods...
}
```

3. **Foreground Service**: A foreground service is a service that's considered to be something the user is actively aware of and thus not a candidate for the system to kill when low on memory. Foreground services must display a Notification. Foreground services continue running even when the user isn't interacting with the app.

```kotlin
class MyForegroundService : Service() {
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        val notification: Notification = // Initialize your notification here
        startForeground(NOTIFICATION_ID, notification)
        return START_STICKY
    }

    // Implement other required methods...
}
```

In terms of **memory management**, services are no different from any other app component in that they can also be shut down by the system if memory is low and if they haven't been used for a while, or if the system must recover memory for more active components. To avoid this, you can promote your service to the foreground.

**State preservation** is not directly handled by the Service component. You need to manage this manually if needed, typically through shared preferences or a database.

**Intents** are used to start services and to pass data between them. They can be explicit (targeting the service directly) or implicit (asking the system to find a suitable service).

```kotlin
// Explicit Intent
val intent = Intent(this, MyService::class.java)
startService(intent)

// Implicit Intent
val intent = Intent()
intent.action = "com.example.MY_ACTION"
startService(intent)
```

Services can **interact with other components**. They can start activities, broadcast receivers, and interact with content providers. They can also start other services.

Remember, managing the lifecycle and state of a service is crucial for building robust Android applications and providing a good user experience.