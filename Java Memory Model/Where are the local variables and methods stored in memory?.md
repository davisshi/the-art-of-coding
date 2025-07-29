Where are the local variables and methods stored in memory?

The stack

Local variables and references are stored in the stack. Primitive data types (like int , double ) live here. Each thread has its own stack, making the stack memory non-shared and thread-specific.

—————————————————————————————
In java, the objects referenced by local variables can live in heap.  Thread local is implemented with threadlocalmap which is allocated in heap.

Check ThreadLocal.java on GitHub/openjdk, you will see the implementation.
—————————————————————————————

Yes, there is a static ThreadLocalMap class inside ThreadLocal class. All the different ThreadLocal objects of a thread are stored as keys in ThreadLocalMap which is a static object allocated in the heap. Actually the usual use case using ThreadLocal is to store the thread context related data, like tracking Id, which is accessible in the whole processing period of the thread.

Actually there are three aspects of variables. First one is the static global variables which are stored in the MetaSpace after Java 8. And second one is the local variables of methods, which are stored in the thread-specific stack. The third one is the Thread Local Variables which are stored in the ThreadLocal <T> variables which are implemented by the thread-specific static ThreadLocalMap and are accessible through the whole processing period of the thread. The ThreadLocalMap object is stored in the heap, however its static reference variable is stored in the MetaSpace since ThreadLocalMap is a static class of ThreadLocal.

One thing needs to pay attention to ThreadLocal is that: ThreadLocal provides an easy-to-use API to confine some values to each thread. This is a reasonable way of achieving thread-safety in Java. However, we should be extra careful when we’re using ThreadLocals and thread pools together. Since the application didn’t perform the necessary cleanups last time, it may re-use the same ThreadLocal data for the new request. We can extend the ThreadPoolExecutor class and remove the ThreadLocal data in the afterExecute() method to solve this issue.


—————————————————————————————
Static classes and static variables are not the same thing. Each thread has its own ThreadLocalMap
—————————————————————————————

Yes, you are right. Static classes are used for grouping classes. Since in Thread class, it declares as: "ThreadLocal.ThreadLocalMap threadLocals = null;", there is no static before ThreadLocal.ThreadLocalMap, so it is an variable of an instance Thread, and each Thread owns its ThreadLocalMap.


1. An Introduction to ThreadLocal in Java
   https://www.baeldung.com/java-threadlocal

2. Introduction to Java’s Memory Model — Heap, Stack, and Metaspace
   https://medium.com/@AlexanderObregon/introduction-to-javas-memory-model-heap-stack-and-metaspace-ceaeb565921c

3. Static variables and methods in Java. Where JVM stores them. Static in Kotlin.
   https://www.linkedin.com/pulse/static-variables-methods-java-where-jvm-stores-them-kotlin-malisciuc/


While local variables on the thread's stack are inherently thread-safe because each thread has its own separate stack, ThreadLocal and ThreadLocalMap serve a different purpose, addressing scenarios where you need:

* Thread-Specific Global-like Variables: . Opens in new tab ThreadLocal allows you to define variables that appear globally accessible within a single thread's execution but are distinct for each thread. This is especially useful for maintaining context, such as user authentication details, transaction IDs, or temporary data that needs to be accessible across multiple method calls within the same thread's scope without explicitly passing it as arguments.   
* Managing Non-Thread-Safe Objects: . Opens in new tab If you have a non-thread-safe object (e.g., SimpleDateFormat, Random) that you want to use in a multi-threaded environment, ThreadLocal provides a way to give each thread its own instance of that object. This eliminates the need for external synchronization and the performance overhead associated with it, as each thread operates on its isolated copy.   
* Avoiding Parameter Propagation: . Opens in new tab In complex call stacks, passing the same "context" object or variable through numerous method parameters can lead to cluttered and less readable code. ThreadLocal offers a cleaner alternative by making this data implicitly available to any method within the same thread's execution.   
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Why not just use the stack?

Local variables on the stack are limited to the scope of the method they are declared in. Once the method returns, these variables are popped off the stack and are no longer accessible. ThreadLocal variables, on the other hand, persist for the entire lifetime of the thread or until explicitly removed, allowing data to be shared across different method calls and even different classes within the same thread's execution. This persistence and wider scope are the key distinctions that make ThreadLocal a valuable tool beyond basic stack-based local variables.
