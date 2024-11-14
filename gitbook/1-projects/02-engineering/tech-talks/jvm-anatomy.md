By Nikita Lipsky 27 yrs exp.


X(twitter) : @pjBooms

- Working for Jetbrains on Compose MPP
- Excelsior Jet JVM with AOT compiler projector initiator



Java books 

1. The JVM specification Second Edition by Tim Lindholm Frank Yellin
2. The Java Language Specification, Second Edition James Gosling Bill Joy


---
Agenda

- Java class file and bytecode 


---
### Java class file and bytecode

java source -> java bytecode 


Class file 
- version
- constant pool
- class name, modifiers
- superclass, superinterfaces
- fields
- methods
- attributes

Example of constant pool

- Constant integer 
- constant float
- constant string 
- constant class 
- Constant field reference
- constant method reference
- constant interface method references


Java class file 

- fields, methods may have attributes
- main attribute of a method is its code : Java bytecode

Java bytecode

- Instructions array
- Operand stack
- Local variables array (method arguments, local variables)


Java is stack machine - intermediate results are stored in stack.

An instruction pops its operands from the operand stack and pushes result back to the stack. 

0: iload 3
2: bipush 5
4: iadd
5: istore 4
..


JVM specifications each instructions is very strictly defined. All JVMs execute same bytecode similarly. 
They massproduce same results. 

Languages like c, c++ doesn't have this behaviour. they are undefined. 


JVM preface

what does any program that runs on a JVM have?

- main : public static void main(String[] args) 
- classpath - list of directories and archives (jar files)
	- or module path since Java 9

It is not enough to have a JVM only to run a java program. Java Runtime Environment is needed for it

- JVM 
- Platform classes 
	- core classes (i.e j.l.Object, j.lString, etc)
	- Java standard APIs (IO, NET, AWT/Swing, etc)
- Implementation of native methods of platform classes (OS specific, distributes as native dynamic libraries - .dll, .so, .dylib)
- Auxiliary files (time zones, locales description, media resources, etc)

![[JVM anatomy.png]]


Class loading engine

JVM executes clases from the following sources 
	- Java Runtime (platform classes)
	- Application classpath
	- Auto generated on-the-fly (Proxy, Reflection accessors, invoke dynamic implementation)
	- Provided by the application itself



Classloading

Every class is loaded by a class loader 
- Platform classes are loaded by the boostrap class loader 
- Classes from application classpath are loaded by the system class loader (AppClassLoader)
- Application classes may create user-defined class loaders
- **Class loader forms a unique class name space.**


JVM can load different classes with same fully qualified name provided they are loaded by different class loaders.


Java 9+ not only has class loaders it also belongs to modules. Better architecture. More read on Java 9 modules. 


JVM startup 

- Main class is loaded by system class loader (from application classpath or modulepath)
	- provokes loading a part of platform classes like j.l.Object and its dependencies. 
- public static void main(String[] args) of the main class is executed. 


Class loading process (creation of a class)

Class file parsing
- Class format is checked on correctness (may throw a ClassFormatError)
Creation of a runtime representation of the class in a special JVM memory area
	- runtime constant pool in Method area aka Meta Space aka Permanent Generation
Loading of a superclass and superinterfaces 


Linking 

- Java bytecode verification
- Preparation
- Resolution of symbolic references

0: bipush 2
2: bipush 2
4: iadd
5: goto 0

Bytecode won't be executed. 
JVM standards are not met for this bytecode. Specifications are not met. Something to do with the stack being not empty. But here its empty. 

Javabytecode verification

- performed once for a class 
- instructions correctness checks (correctness of branches)
- operand stack and local variables out of bounds check 
- Type assign compatibility checks


$java -Xverify:none test

Stackoverflow error will hapen in the JavaRuntime environment. Internal error javaCalls.cpp will fail. 

Don't disable verifier if you dont want to see crashes like this!


Class initialisation 

Call of a class static initialiser 

```

class A {
static int i = 10;
static String s = "Arun";
static {
System.out.println(s);
}
}

A.class 
...
<clinit>;
i=10;
s="Arun"
System.out.println(s);
...

```

Class initialisation

- Happens on a first use
	- new 
	- static field access
	- static method call
- Provokes initialization of a super class and super interfaces with default methods


**Java bytecode exectuion** 

JVM may execute bytecode via 

- Interpretation
- Translation (Compile) into native code, that will run directly on CPU


Interpreter
pc = 0
do {
fetch opcode at pc;
if(operands) fetch operands;
execute the opcode;
calculate pc;
} while(there is more to do so);

Eg. Hotspot JVM (0 interpreter) Very slow

Modern JVMs use Template interpreter

-  every bytecode instructions is implemented as a sequence of target CPU instructions (template)
- Instruction interpretation is just jump to corresponding templates


**Compilers**
So translating to native instructions will be much faster than interpretation.
- Non-Optimising 
- Simple optimising (hotspot client C1)
- Sophisticated optimising (hotspot server C2)


Compilers 

Dynamic (Just-In-Time - **JIT**)
- Translate into native code happens at application runtime
Static (Ahead-Of-Time - **AOT**)
- Translation happens before program execution



Dynamic compiler (JIT)

- work concurrently with program execution
- compile hot code only
- hot code is determined by means of profiling
- profiling information is used for optimal optimizations (speculative)

Static Compilers (AOT)

- are not limited in resources for optimisations
- compile every method of a program using the most aggresive optimisations
- no overheads at runtime (fast startup)


If a java program is compiled statically, it may happen that no bytecode will be executed at runtime.



Reflection 

- allows access to classes, fields, methods via name (by string literal) from a java program
- is implemented in the JVM via access to Meta Space
- Key feature of a java for many popular frameworks and JVM based programming lang implementations (groovy, clojure, Ruby, etc.)


Method handles and invokedynamic (JSR-292, indy)

Indy: programmable call 
- for effective implementations of dynamic programming languages on the JVM 
- Used for lambda objects creation, string concatenation
MethodHandle - target object of invokedynamic call 
- can be an access to a field, a method
- combination of other method handles 
- can be used independently from indy: reflection 2.0


Java Native Interface (JNI)

- Binds the JVM with the outside world (OS)
- C interface to the JVM 
	- does not depend on the implementation details of the JVM
	- is used for implementation of native method in C language or any other low level language. 
	- JNI is used to implement platform specific parts of Java SE API: IO, NET, AWT.
- JNI is implemented in the JVM space as an acess to Meta space.


Project panama 

C interop without coding in C
- Direct external C functions calls from Java
- C data structures access from Java


Threading and Synchronisation 

Multithreading is key feature of Java platform 
Makes use of modern hardware. Some dynamic language doesn't support multi threading


java.lang.Thread

- java thread is mapped to a native thread in a 1-1
- Each thread has a reserved region of memory referred to as its stack containing local variables and operands stack of methods (method frames) being executed within the thread. 
	- Thread stack size is a JVM argument: -Xss
- Java thread has a detailed information about its stack (stack trace) 
	- You may print or examine stack from a java program!

- At any time, the stack might contain natively compiled method frames. 

Native threads are expensive since there is a limitation imposed on how many can be created. 

Project Loom 

Problem: There are limitations of how many native threads can be created (native threads are expensive)

Solution: **virtual threads** (light-weight threads) managed by the JVM (quitting 1-1 scheme)



Exception handling 

So JVM knows everything about the call stack, it helps it in exception handling implementation. 

![[exceptional-handling-in-JVM.png]]



Threads and Java memory model 

Thread 1; 
```
shared.data = getData();
shared.ready = true;
```

Thread 2;
```
while(!shared.ready) {
//wait
}
data = shared.data;
```

JVM might optimise the code and set the ready to true at the compile time itself then it breaks the logic. 
Solution: Use volatile!



Synchronization

- For safe access to a shared memory between threads
- Naive implementation may use OS synchronization primitives
	- Java object has a OS monitor as a hidden field 
- Highly optimised when a resource contention happens less rarely than an enter to synchronised block 
- Today its recommended to use java.util.concurrent primitives instead of built-in synchronisation.



Memory management - Memory Allocation 

- Implemenation of the new operator
- Objects allocated with the new operator reside in so called Java heap
- Java heap structure is JVM implementation specific. 
- Java objects layout is JVM implementation specific as well. 
- Garbage collection algorithm is also JVM specific. 
  JVM specifications only say that garbage may be collected. 

- Must be fast
	- JVM queries OS for memory for many objects at once not for one
	- Allocation by bump the pointer technic
- Must be thread-safe but parallel (non-blocking)
	- Thread local heaps; every thread consumes thread local memory region
Object allocation (memory) is a heap restructure operation which means it must be put on a lock before modification. Therefore each thread has its own local heap.



Java Object Layout

The layout is not specified by the JVM however requires 
- Java Object Header
		- Reference to a class object
		- Monitor (lock word)
		- Identity hashcode
		- GC flags
- Fields
		- May be reordered in sake of size optimisations, alignment, or target architecture specifics.



Project Valhala

- The main idea is to introduce the concept of objects in the JVM, which don't require a header at all. 
	- Object erasure to its primitive data types
	- removing unnecessary indirection in arrays

Code like a class, works like an int.



**Garbage Collection**

what is garbage? 
my definition: Some object that is disconnected from the GC roots. 


Garbage are objects that cannot be used by a program

Not garbage:
1. Objects in static fields of classes
2. Objects in local variables, operand stack (method frame)
3. Objects that are referenced by "not garbage".

GC roots
1. Objects in static fields of classes
2. Objects that are accessible from thread stacks
3. Objects that are referenced by JNI references in native methods. 


**Live Objects**
1. Objects from GC roots 
2. Objects that are referenced by live objects.
Everything else is garbage.

Tracing garbage collectors

- Mark and sweep 
	- mark live objects, sweeps (frees) the garbage

- Stop and copy
	- heap is divided into two semi-spaces
	- copies live objects to the second semi-space
	- first semi-space is used as second semi-space on the next collection.


**Stop the world**
- Live objects are defined for a specific moment of a program execution: that set of live objects is being changed during the execution.
- To collect the garbage, all the threads should be paused to determine the garbage(STW pause).

Java is criticised for GC pauses. 


One of the main tasks of modern GC is to reduce the STW pause. Methods to reduce that:

- Incremental
	- do no collect all the garbage within the GC pause
- Parallel
	- collect the garbage in parallel threads within GC pause
- Concurrent
	- collect the garbage concurrently within program execution


Generational Garbage Collection

Weak generational hypothesis
- Most objects die young
- Old objects rarely reference young object

Generational GC:
- Particular case of incremental GC
- During minor collection cycles, only young objects are traced. 
- Objects that survived cycles are moved to older generation


Fully concurrently GC - ZGC 


Thread local Garbage Collection

Thread local hypothesis:
- Most objects die in a thread that create them.

Thread local GC
- Collect thread local garbage within a respective thread not pausing other threads. 

promising idea! 

Book; the garbage collection handbook.


Manageability & Monitoring

JVM knows everything about your Java program
- about all loaded classes
- about all live objects
- about all threads
- about all methods that are executed within threads


JVM tool interface (JVM TI)
- debuggers 
- profilers

Java Management Beans
- real time monitoring tools 
	- JConsole, JMX console, AMC
	- Visual JM
	- Java Mission Control

JVM Implementations

- Oracle HotSpot (OpenJDK)
- IBM J9 (Open J9)
- Oracle JRockit (RIP)
- Excelsior JET(RIP)
- Azul Zing (Hotspot based, but has its own GC and LLVM-based JIT)
- GraalVM (Hotspot based, has JIT implementation written in Java)
- Liberica (Bellsoft), Amazon, Microsoft, SAP, RedHat, JetBrains runtime (builds of OpenJDK with possible changes).


Conclusion

- JVM is quite sophisticated but very interesting thing
- Java is golden mean of modern IT tech
	- Strictly specified in every detail
	- efficiently multiplied by flexibility
- All JVM implementations are constantly evolving at the cutting edge of science and technology. 
GC, Compiler are scientific researches. All open source!

