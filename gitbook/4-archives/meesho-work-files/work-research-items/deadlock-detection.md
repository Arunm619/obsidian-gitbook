
Issues with multithreading can be really difficult to identify and resolve. It's essential to have a mechanism that automates this process and allows for the monitoring of deadlock identification. This document explains how to capture details about deadlocks.


Before getting started about capturing the issues let's take a look at the issues with examples.

1. Multiple thread blocks (possibly Deadlocks)
2. Single Long blocks 

#### Deadlocks


A deadlock is a situation where two or more threads are blocked forever, waiting for each other. This usually happens when multiple threads need the same locks but obtain them in different order. If a thread holding locks on multiple objects releases them in a different order than they were requested, deadlock can occur.


We will create two different resources for the threads to work with.
```kotlin
val resource1 = Any()
val resource2 = Any()
```


Both the threads needs `resource1` and `resource 2` to finish their work. 
Here, thread1 acquires the lock for `resource1` and waits for sometime (intentionally) before acquiring the lock for `resource2`. But in that gap, `thread2` acquires the lock for `resource2` and starts waiting for the `resource1`. Deadlock is now created and they will both keep waiting for the resources indefinitely.
```kotlin
val thread1 = Thread {
    synchronized(resource1) {
        Thread.sleep(100) // Give thread2 a chance to lock resource2
        synchronized(resource2) {
            // Work that requires both resource 1 and resource 2
            // Code here will never be reached
        }
    }
}

val thread2 = Thread {
    synchronized(resource2) {
        Thread.sleep(100) // Give thread1 a chance to lock resource1
        synchronized(resource1) {
            // Work that requires both resource 1 and resource 2
            // Code here will never be reached
        }
    }
}

thread1.start()
thread2.start()
```


Problems with deadlock:

1. **Performance Degradation**: Deadlocks can lead to application freezing, slow performance, and high CPU usage. This is because threads are stuck in an indefinite waiting state for resources locked by each other, causing the CPU to be constantly engaged.

2. **Unstable Application State**: Deadlocks can result in an inconsistent application state, unpredictable behavior, and even application crashes. This is particularly true if a deadlock occurs during a critical operation, making the app unstable and difficult to debug due to the unpredictable nature of deadlocks.

3. **Negative User Experience**: The performance issues and instability caused by deadlocks can lead to a poor user experience. This can result in negative reviews, uninstalls, and overall dissatisfaction among users.


----

#### Long blocking threads

Long blocking threads refer to threads that are blocked or waiting for a long period of time. This can occur due to various reasons such as waiting for I/O operations to complete, waiting for a lock to be released, or waiting for a condition to be met using methods like `Object.wait()`.

```Kotlin
val monitor = Object()  
  
val thread1 = thread(start = false) {  
    synchronized(monitor) {  
        try {  
            Timber.d("Thread 1 is waiting")  
            monitor.wait()  
            Timber.d("Thread 1 is resumed")  
        } catch (e: InterruptedException) {  
            e.printStackTrace()  
        }  
    }  
}  
  
val thread2 = thread(start = false) {  
    synchronized(monitor) {  
        try {  
            Thread.sleep(7000)  
            // monitor.notify() OOPS forgot to notify 
            Timber.d("Thread 2 notified (actually not)")  
        } catch (e: InterruptedException) {  
            e.printStackTrace()  
        }  
    }  
}  
thread1.name = "Thread 1"  
thread2.name = "Thread 2"  
  
  
thread1.start()  
thread2.start()
```


 `thread1` is a long blocking thread because it calls `monitor.wait()`, which causes it to wait indefinitely until another thread calls `monitor.notify()` or `monitor.notifyAll()`. However, here `thread2` never calls `monitor.notify()`, so `thread1` will remain blocked.

Long blocking threads can lead to performance issues, as they tie up system resources without doing any useful work. They can also lead to deadlock situations if multiple threads are waiting for each other to release locks. Therefore, it's important to manage threads carefully in concurrent programming to avoid these issues.

-----

These kind of misbehaving threads can cause undefined states in the application which can in turn cause ANRs, OOMs and other negative experiences for the user. 



###### How to solve for these issues in the app?

Observation is the key. 

```
If you can't measure it, you can't improve it. 
									 - Lord Kelvin
```


Likewise, we need a way to start tracking it.

`DeadLockDetector` does exactly this.


On a high level, this class works by periodically polling all active threads in the application and checking their state. If it finds multiple threads that are blocked or waiting, it logs this information as it could indicate a potential deadlock. 


We consider an thread to be waiting when it is having the internal state as 
- Thread.State.WAITING
- Thread.State.TIMED_WAITING



```Kotlin
/**  
 * A class that polls active threads at a set interval and logs when multiple threads are BLOCKED. */

class DeadlockDetector(private val handler: Handler, private val pollingInterval: Long) {  
  
    private var running = false  
    private val previouslyBlocked: MutableSet<Long> = mutableSetOf()  
    private val waitingStates: Set<Thread.State> = setOf(Thread.State.WAITING, Thread.State.TIMED_WAITING)  
  
    @Volatile var lastThreadDump: Map<Thread, Array<StackTraceElement>>? = null  
  
    @Volatile var lastThreadDumpTime: Long = -1  
  
    fun start() {  
        Timber.d("Arun, Beginning deadlock monitoring.")  
        running = true  
        handler.postDelayed(this::poll, pollingInterval)  
    }  
  
    fun stop() {  
        Timber.d("Arun, Ending deadlock monitoring.")  
        running = false  
        handler.removeCallbacksAndMessages(null)  
    }  
  
    private fun poll() {  
        Timber.d("Arun, Polling for deadlocks.")  
        val time: Long = System.currentTimeMillis()  
        val threads: Map<Thread, Array<StackTraceElement>> = Thread.getAllStackTraces()  
        Timber.d("Arun, threads size: ${threads.size}")  
        val blocked: Map<Thread, Array<StackTraceElement>> = threads.filter { entry ->  
            val thread: Thread = entry.key  
            val stack: Array<StackTraceElement> = entry.value  
  
            thread.state == Thread.State.BLOCKED || (thread.state.isWaiting() && stack.hasPotentialLock())  
        }.filter { entry -> !BLOCK_BLOCKLIST.contains(entry.key.name) }  
  
        val blockedIds: Set<Long> = blocked.keys.map(Thread::getId).toSet()  
        val stillBlocked: Set<Long> = blockedIds.intersect(previouslyBlocked)  
  
        if (blocked.size > 1) {  
            Timber.d(buildLogString("Arun, Found multiple blocked threads! Possible deadlock.", blocked))  
            lastThreadDump = threads  
            lastThreadDumpTime = time  
        } else if (stillBlocked.isNotEmpty()) {  
            val stillBlockedMap: Map<Thread, Array<StackTraceElement>> = stillBlocked.map { blockedId ->  
                val key: Thread = blocked.keys.first { it.id == blockedId }  
                val value: Array<StackTraceElement> = blocked[key]!!  
                Pair(key, value)  
            }.toMap()  
  
            Timber.d(  
                buildLogString(  
                    "Arun, Found a long block! Blocked for at least $pollingInterval ms.", stillBlockedMap  
                )  
            )  
            lastThreadDump = threads  
            lastThreadDumpTime = time  
        }  
  
        previouslyBlocked.clear()  
        previouslyBlocked.addAll(blockedIds)  
  
        if (running) {  
            handler.postDelayed(this::poll, pollingInterval)  
        }  
    }  
  
    private fun Thread.State.isWaiting(): Boolean {  
        return waitingStates.contains(this)  
    }  
  
    private fun Array<StackTraceElement>.hasPotentialLock(): Boolean {  
        return any {  
            it.methodName.startsWith("lock") || (it.methodName.startsWith("waitForConnection"))  
        }  
    }  
  
    companion object {  
        private var deadlockDetector: DeadlockDetector? = null  
        private val LOCK = Any()  
        fun getDeadlockDetector(handler: Handler, toMillis: Long): DeadlockDetector {  
            if (deadlockDetector == null) {  
                synchronized(LOCK) {  
                    if (deadlockDetector == null) {  
                        deadlockDetector = DeadlockDetector(handler, toMillis)  
                    }  
                }  
            }  
            return deadlockDetector!!  
        }  
  
        private val TAG = "DeadlockDetector"  
  
        private val BLOCK_BLOCKLIST = setOf("HeapTaskDaemon")  
  
        private fun buildLogString(  
            description: String, blocked: Map<Thread, Array<StackTraceElement>>  
        ): String {  
            val stringBuilder = StringBuilder()  
            stringBuilder.append(description).append("\n")  
  
            for (entry in blocked) {  
                stringBuilder.append("-- [${entry.key.id}] ${entry.key.name} | ${entry.key.state}\n")  
  
                val stackTrace: Array<StackTraceElement> = entry.value  
  
                for (element in stackTrace) {  
                    stringBuilder.append("$element\n")  
                }  
  
                stringBuilder.append("\n")  
            }  
  
            return stringBuilder.toString()  
        }  
  
    }  
}
```




###### Conclusion

With this detector in place, we can capture the issues immediately as they occur and fix them and prevent them from happening again.

----

