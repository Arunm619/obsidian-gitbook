
Memory Leaks 


LeakCanary Inception 2015
AKA Memory Diaper (LOL)


Default go to lib: Timber, StrictMode, later LC. 


Payment Terminal App built in square. 
It was running 24*7 and when memory grows it becomes a problem. 
So LeakCanary was invented. 

----


Java days - Memory Analysis Tool - Eclipse Mat - Heap Dump Analysis. 

Heap dumps - Looking for object and trying to find whats held in memory by computing whats called the shortest pass from GC roots to the object.

Open source eclipse MAT code was taken and adapted to android to run locally and v1 of LC was born.


Eclipse impl to android studio Memory analyser (meant for desktop) which was not so great ( even for desktop) to Own implementation suitable for phone device. 


---
High level

LeakCanary is a memory leak detection library for Android and Java. It works by watching for objects that should be garbage collected and then reporting these objects if they are still in memory after a period of time, indicating a memory leak.

Here's a simplified overview of how LeakCanary analyzes HPROF files:

1. **Heap Dump**: When LeakCanary detects a potential memory leak (an object that should have been garbage collected but wasn't), it triggers the Android Runtime to create a heap dump, which is an HPROF file.

2. **Heap Analysis**: LeakCanary then analyzes this HPROF file. It starts by looking for a specific set of objects in the heap dump that it knows should have been garbage collected. These are typically objects that are tied to the lifecycle of an Activity or Fragment, such as Views, Contexts, etc.

3. **Shortest Path to GC Roots**: For each of these objects, LeakCanary then computes the shortest path to GC Roots. GC Roots are objects that are always reachable and can't be garbage collected. This path represents the chain of references that is preventing the object from being garbage collected.

4. **Leak Reporting**: If LeakCanary finds a path from the object to the GC Roots, it means the object is leaking. LeakCanary then generates a leak trace, which is a representation of the path from the leaking object to the GC Roots. This leak trace is then reported to the user.

It's important to note that LeakCanary doesn't fix the leaks. It only reports them. It's up to the developer to use the information provided by LeakCanary to find and fix the memory leaks in their code.

The actual process is more complex and involves dealing with many edge cases and optimizations to make the process faster and more accurate. For a more detailed understanding, you can look at the source code of LeakCanary on GitHub.


**Internal Implementation***


Activity Watcher 
With the application instance and register activity lifecycle callbacks.


we care about only one `OnActivityDestroyed

Java dynamic proxy is used for delegating it with NoOp Implementation. (Retrofit working)

---
Java Dynamic Proxy Example


```Kotlin
package leakcanary.internal

import java.lang.reflect.InvocationHandler
import java.lang.reflect.Proxy

internal inline fun <reified T : Any> noOpDelegate(): T {
  val javaClass = T::class.java
  return Proxy.newProxyInstance(
    javaClass.classLoader, arrayOf(javaClass), NO_OP_HANDLER
  ) as T
}

private val NO_OP_HANDLER = InvocationHandler { _, _, _ ->
  // no op
}
```
Source - [leakcanary/leakcanary/leakcanary-android-utils/src/main/java/leakcanary/internal/Objects.kt at b5e059c8f8323f1df5f43127e8a55d9f3cdf7dd4 · square/leakcanary · GitHub](https://github.com/square/leakcanary/blob/b5e059c8f8323f1df5f43127e8a55d9f3cdf7dd4/leakcanary/leakcanary-android-utils/src/main/java/leakcanary/internal/Objects.kt#L6)
This Kotlin code is creating a "no-op" (no operation) delegate for a given type T. This is often used in situations where you want to provide a default implementation of an interface that does nothing (hence, "no-op"). 

Let's break it down:  

 - `internal inline fun <reified T : Any> noOpDelegate(): T` This is an inline function that takes a reified type parameter T. The reified keyword allows the function to access the type T at runtime, which is not normally allowed in inline functions. The function returns an instance of T.  
- `val javaClass = T::class.java: This gets the Class object for the type T` This is needed to create a new proxy instance.  
- `Proxy.newProxyInstance(javaClass.classLoader, arrayOf(javaClass), NO_OP_HANDLER) as T` This creates a new proxy instance that implements the interface T. The proxy instance will use the NO_OP_HANDLER to handle all method calls.  
- `private val NO_OP_HANDLER = InvocationHandler { _, _, _ -> }`: This is an InvocationHandler that does nothing. Whenever a method is called on the proxy instance, this handler will be invoked. In this case, it simply ignores all method calls.  
- 
Here's an example of how you might use this function:


interface MyInterface {
    fun doSomething()
    fun doSomethingElse()
}

fun main() {
    val myInterface: MyInterface = noOpDelegate()
    myInterface.doSomething()      // Does nothing
    myInterface.doSomethingElse()  // Does nothing
}

----

Similar to Retrofit.


What should happen when an activity is destroyed. 
When we want to talk with the java world, we should tell that the expectation is the destroyed activity objects should be unreachable or weakly reachable i.e There should be no strong reference from any of the GC roots. 

GC root - Java class static fields 

If you put something in the static field, it will never be garbage collected. 

Any objects that are reachable from the strong references can never be garbage collected. 



Memory is a graph
Whenever the activity is destroyed, the entire objects referenced from the activity should be removed in the graph and should become unreachable


ActivityWatcher logic 
Needs app instance and DeletableObjectReporter with below signature


```kotlin
interface DeletableObjectReporter{
	fun expectDeletionFor(  
	  target: Any,  
	  reason: String  
	) : TrackedObjectReachability
}
```


WeakReference - JDK class

Reference
4 types
- Phantom Reference
- Final Reference
- Weak Reference 
- Strong Reference

In Java, a reference is a way to access or 'refer to' an object. The Java Development Kit (JDK) provides a package `java.lang.ref` that contains classes for reference objects. Reference objects allow you to interact with the garbage collector in a more sophisticated way than just by creating and discarding objects.

Here's a brief overview of the classes in the `java.lang.ref` package:

- `Reference`: This is the base class for all reference objects. It defines common behavior for all reference objects.

- `SoftReference`: A soft reference is a reference that isn't as strong as a normal reference. The garbage collector might decide to reclaim a softly reachable object, but it's guaranteed to do so before throwing an `OutOfMemoryError`.

- `WeakReference`: A weak reference is weaker than a soft reference. The garbage collector will reclaim a weakly reachable object as soon as no strong or soft references to the object remain.

- `PhantomReference`: A phantom reference is the weakest of all. You can't retrieve the object a phantom reference refers to. The only use of such a reference is keeping track of when it gets enqueued into a `ReferenceQueue`, as at that point you know the object to which it pointed is dead.

- `ReferenceQueue`: This is a queue to which registered reference objects are appended by the garbage collector after the appropriate reachability changes are detected.

These classes provide a way to interact with the garbage collector, allowing for more sophisticated memory and object lifecycle management than is possible with simple object creation and destruction.

---

Read about GC in the JVM here - [How Garbage Collection works in Java? Explained](https://javarevisited.blogspot.com/2011/04/garbage-collection-in-java.html)

----
Bob Lee - Different type of references 
[The Ghost in the Virtual Machine: A Reference to References - YouTube](https://www.youtube.com/watch?v=KTC0g14ImPc)

---


Weak references basically mean the object referenced by it will keep it until there are no strong references to it and when it becomes isolated with no strong ref, then GC may or may not set the reference to NULL

So the activity watcher will add the weak reference for the activity and check if it has been actually removed and made weakly reachable if not it is considered retained and invoke the object retained callback.

```kotlin
private fun moveToRetained(key: String) {  
  removeWeaklyReachableObjects()  
  val retainedRef = watchedObjects[key]  
  if (retainedRef != null) {  
    retainedRef.retainedUptimeMillis = clock.uptime().inWholeMilliseconds  
    onObjectRetainedListener.onObjectRetained()  
  }  
}
```

Basically an object which was supposed to garbage collected (weak reference) was not actually weak reference (strong ref duh) therefore we reported it.

Once we get this callback LC can actually start doing things. 


Uber used this logic to capture the objects count.
This has no runtime overhead. 

---

In v1 of LC, because of android leaks, the heap dumps was too much. So a baseline threshold was set : Min 5 objects must be leaking. 


Can't have whitelist because we can't know the type of the leaks until we actually dump the heaps. So we can't dump everytime when there is a leak (Android OS failure)

---
Dump heaps 

GC Trigger code is run.

```Kotlin
private fun runGc() {  
  // Code taken from AOSP FinalizationTest:  
  // https://android.googlesource.com/platform/libcore/+/master/support/src/test/java/libcore/java/lang/ref/FinalizationTester.java  // System.gc() does not garbage collect every time. Runtime.gc() is  // more likely to perform a gc.  
  Runtime.getRuntime().gc()  
  enqueueReferences()  
  System.runFinalization()  
}
```

Actually runs. Even though not guaranteed. Its a secret.

---
What is dumping the heap?

In the VM we have the heap which is just a block of memory. Heap is just a list of objects like everything else in Java. 

Every object has a memory assigned some bytes , some reference to another object. 

GC roots - start from the list of objects.
Navigates the references from the start and thats how it finds all the objects that are meant to be in the memory and everything else gets removed. 

### Hprof#Dump() 
void Dump() 

essentially goes thru the list of objects in memory and dumps it in the file. 

1. Process Heap 
2. Visit roots
3. Visit Image Roots
4. Dump heap object
Copies the objects from memory and dumps into a file. Thats why its freezing. 

---

HeapDumper#dumpHeap

A better way in terms of time and memory to copy memory into file is forking. 

When forking from parent, the child fork copies all the memory which we can use to dump.

They hack into the memory and find the method reference and call it. The merit is we can get the heap dumped without any freeze. This is hacky solution and stopped working in the most recent ones. Different for ARM and X86

Chinese coder rocks! swap the heap dumper with your own impl.

---


Now we have heap dumped onto the disk. 
We gotta analyse it next.

if progaurd enabled builds, we also hook in progaurd mapping file 

We parse the header info from the file. 
Hprof version,
Heap Dump Time Stamp,
identifier byte size (32 or 64 bits)


Hprof Files: 
List of objects in order 
Object: Id, type, bunch of bytes

MAT like tools use in memory nodes to represent the graph like structure for representing the connections and references. 

but is very costly in terms of memory.

Indexing the object location in file in the memory to fast access instead of loading all the objects as nodes in memory. 

`HprofInMemoryIndex` stores the index of an object from the hprof file.

---
An HPROF file is a binary heap dump file format in Java. It's used for heap profiling and is generated by the Java Virtual Machine (JVM) when it's instructed to do so, typically when an OutOfMemoryError is thrown. It contains information about the Java objects and classes in the heap at the moment the snapshot is triggered. 

Because an HPROF file is a snapshot of the heap memory, it is used to debug memory issues, including memory leaks and high memory consumption. Tools like Eclipse Memory Analyzer (MAT) or VisualVM can be used to analyze HPROF files.

Here's an example of how to generate an HPROF file:

```java
public class GenerateHprof {
    public static void main(String[] args) throws Exception {
        List<String> list = new ArrayList<>();
        while (true) {
            list.add("OutOfMemoryError soon");
            Thread.sleep(1);
        }
    }
}
```

When you run this program, it will eventually throw an `OutOfMemoryError`. If you run this program with the `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/path/to/dump.hprof` JVM options, it will generate an HPROF file at the specified path when the `OutOfMemoryError` is thrown. 

Please note that the generated HPROF file can be quite large (as it's a snapshot of all the objects in the heap), so ensure you have enough disk space where you're generating it.

----


Graph APIs:
Fields, Objects, Instances, Primitives, etc. 

Find all weak references and Find Leaking Object Ids

Graph traversal : Shortest path (BFS) from object to GC root.


---

3.0 - updates
- New UI 
- TreeMap Visualisations
- Compose for desktop app

