
**Process vs Thread: Understanding the Difference**

To comprehend the dissimilarities between a process and a thread, it's crucial to grasp the fundamental concepts of a program, process, and thread.

**Program**:
- A program is an executable file containing a set of processor instructions stored on disk.
- When loaded into memory and executed by the processor, it becomes a process.

**Process**:
- A process encompasses the code from a program along with the resources required for execution, managed by the operating system.
- Resources include processor registers, program counters, stack pointers, and memory pages allocated for the process's heap and stack.
- Notably, each process possesses its own distinct memory address space, ensuring isolation from other processes. Hence, if one process malfunctions, others remain unaffected.
- Chrome's utilization of process isolation exemplifies this, with each tab operating within its own process.

**Thread**:
- A thread represents the unit of execution within a process, with every process having at least one main thread.
- It's common for a process to encompass multiple threads, each having its own stack.
- Registers, program counters, and stack pointers primarily pertain to threads rather than processes.
- Threads within a process share the same memory address space, facilitating communication through shared memory. However, a malfunctioning thread can potentially compromise the entire process.

**Context Switching**:
- Context switching is the mechanism through which the operating system manages the execution of threads and processes on the CPU.
- During a context switch, the current running process is paused, its state is saved, and another process is allowed to execute.
- This process involves saving and loading of registers, switching memory pages, and updating kernel data structures, making it resource-intensive.
- Switching execution between threads within a process also necessitates context switching. However, it's generally faster compared to switching between processes due to fewer states to track and shared memory address space.
- To minimize context switching overhead, alternative mechanisms such as fibers and coroutines are employed. These methods aim to reduce complexity and enhance performance by cooperatively scheduling tasks, wherein the application manages task scheduling and ensures periodic yielding during long-running tasks.

In summary, while both processes and threads are integral to program execution, they differ in terms of resource allocation, memory isolation, and execution context management, with context switching playing a pivotal role in orchestrating their execution on the CPU.