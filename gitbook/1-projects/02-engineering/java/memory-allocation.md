The Java Virtual Machine (JVM) handles memory allocation through a process that involves several key areas of memory, namely the heap, the stack, the metaspace, and the code cache. Here's a detailed explanation:

1. **Heap**: This is the runtime data area from which memory for all class instances and arrays is allocated. The heap is created on virtual machine start-up and may increase or decrease in size during application run time. When the heap becomes full, garbage is collected. During the garbage collection, objects that are no longer used are cleared, thus making space for new objects.

2. **Stack**: Each JVM thread has a private JVM stack, created at the same time as the thread. A JVM stack stores frames. A frame is used to store data and partial results, as well as to perform dynamic linking, return values for methods, and dispatch exceptions. A new frame is created each time a method is invoked and is destroyed when the method invocation is complete.

3. **Metaspace**: This memory space holds class definitions and other meta-information. The metaspace is created when the JVM starts up. The metaspace can dynamically resize (increase or decrease) at runtime as the classes are loaded and unloaded.

4. **Code Cache**: The JVM also has a code cache, which is used for compilation and storage of native code.

When a Java application creates an object instance at runtime, the JVM automatically allocates memory space on the heap for that object. The Java garbage collector is a program that manages the heap and automatically reclaims memory that is no longer needed. 

To allocate memory, the JVM will first check if there's enough space in the heap to allocate the object. If there's enough space, the JVM will proceed with the allocation. If there's not enough space, the JVM will attempt to reclaim memory that's no longer in use by running the garbage collector. If there's still not enough memory after the garbage collection, the JVM will throw an OutOfMemoryError.