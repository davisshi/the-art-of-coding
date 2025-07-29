[An Introduction to ThreadLocal in Java](https://www.baeldung.com/java-threadlocal)
======================================

Last updated: February 15, 2025

![](https://secure.gravatar.com/avatar/f7bfa7ac878afa29edaf04960cdc924cd1d8228a4dbc84dbd410e20fb76b2e4c?s=50&r=g)

Written by:[baeldung](https://www.baeldung.com/author/baeldung "Posts by baeldung")

-   [Java Concurrency](https://www.baeldung.com/category/java/java-concurrency)

-   [Java Concurrency Basics](https://www.baeldung.com/tag/java-concurrency-basics)

-   [Threads](https://www.baeldung.com/tag/threads)

![announcement - icon](https://www.baeldung.com/wp-content/uploads/2022/04/announcement-icon.png)

Handling concurrency in an application can be a tricky process with many potential pitfalls. A solid grasp of the fundamentals will go a long way to help minimize these issues.

Get started with understanding multi-threaded applications with our Java Concurrency guide:

[>> Download the eBook](https://www.baeldung.com/eBook-Java-Concurrency-NPI-1-Hgj18)

1\. [Overview](https://www.baeldung.com/java-threadlocal#overview)
------------------------------------------------------------------

In this tutorial, we'll be looking at the *[ThreadLocal](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/ThreadLocal.html)* construct from the *java.lang *package. This gives us the ability to store data individually for the current thread and simply wrap it within a special type of object.

2\.[ *ThreadLocal* API](https://www.baeldung.com/java-threadlocal#threadlocal-api)
----------------------------------------------------------------------------------

The *TheadLocal *construct allows us to store data that will be accessible only by a specific thread.

Let's say that we want to have an *Integer* value that will be bundled with the specific thread:

```
ThreadLocal<Integer> threadLocalValue = new ThreadLocal<>();
```

Next, when we want to use this value from a thread, we only need to call a *get()* or *set()* method. Simply put, we can imagine that *ThreadLocal* stores data inside of a map with the thread as the key.

As a result, when we call a *get()* method on the *threadLocalValue*, we'll get an *Integer* value for the requesting thread:

```
threadLocalValue.set(1);
Integer result = threadLocalValue.get();
```

We can construct an instance of the *ThreadLocal* by using the *withInitial()* static method and passing a supplier to it:

```
ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 1);
```

To remove the value from the *ThreadLocal*, we can call the *remove()* method:

```
threadLocal.remove();
```

To see how to use the *ThreadLocal* properly, we'll first look at an example that doesn't use a *ThreadLocal*, and then we'll rewrite our example to leverage that construct.

3\. [Storing User Data in a Map](https://www.baeldung.com/java-threadlocal#storing-user-data-in-a-map)
------------------------------------------------------------------------------------------------------

Let's consider a program that needs to store the user-specific *Context* data per given user id:

```
public class Context {
    private String userName;

    public Context(String userName) {
        this.userName = userName;
    }
}
```

We want to have one thread per user id. We'll create a *SharedMapWithUserContext* class that implements the *Runnable* interface. The implementation in the *run()* method calls some database through the *UserRepository* class that returns a *Context* object for a given *userId*.

Next, we store that context in the *ConcurentHashMap* keyed by *userId*:

```
public class SharedMapWithUserContext implements Runnable {

    public static Map<Integer, Context> userContextPerUserId
      = new ConcurrentHashMap<>();
    private Integer userId;
    private UserRepository userRepository = new UserRepository();

    @Override
    public void run() {
        String userName = userRepository.getUserNameForUserId(userId);
        userContextPerUserId.put(userId, new Context(userName));
    }

    // standard constructor
}
```

We can easily test our code by creating and starting two threads for two different *userIds,* and asserting that we have two entries in the *userContextPerUserId* map:

```
SharedMapWithUserContext firstUser = new SharedMapWithUserContext(1);
SharedMapWithUserContext secondUser = new SharedMapWithUserContext(2);
new Thread(firstUser).start();
new Thread(secondUser).start();

assertEquals(SharedMapWithUserContext.userContextPerUserId.size(), 2);
```

4\. [Storing User Data in *ThreadLocal*](https://www.baeldung.com/java-threadlocal#storing-user-data-in-threadlocal)
--------------------------------------------------------------------------------------------------------------------

We can rewrite our example using a shared *ThreadLocal* instance. Each thread will have its own *Context* stored in the *ThreadLocal* object.

When using *ThreadLocal*, we need to be very careful because every object stored in *ThreadLocal* is associated with a specific thread. In our example, we have a dedicated thread for each particular *userId*, and this thread is created by us, so we have full control over it.

The *run()* method will fetch the user context and store it into the *ThreadLocal* variable using the *set()* method:

```
public class ThreadLocalWithUserContext implements Runnable {

    private static ThreadLocal<Context> userContext
      = new ThreadLocal<>();
    private Integer userId;
    private UserRepository userRepository = new UserRepository();

    @Override
    public void run() {
        String userName = userRepository.getUserNameForUserId(userId);
        userContext.set(new Context(userName));
        System.out.println("thread context for given userId: "
          + userId + " is: " + userContext.get());
    }

    // standard constructor
}
```

We can test it by starting two threads that will execute the action for a given *userId*:

```
ThreadLocalWithUserContext firstUser
  = new ThreadLocalWithUserContext(1);
ThreadLocalWithUserContext secondUser
  = new ThreadLocalWithUserContext(2);
new Thread(firstUser).start();
new Thread(secondUser).start();
```

After running this code, we'll see on the standard output that* ThreadLocal* was set per given thread:

```
thread context for given userId: 1 is: Context{userNameSecret='18a78f8e-24d2-4abf-91d6-79eaa198123f'}
thread context for given userId: 2 is: Context{userNameSecret='e19f6a0a-253e-423e-8b2b-bca1f471ae5c'}
```

We can see that each of the users has its own *Context*.

5\.[ *ThreadLocal*s and Thread Pools](https://www.baeldung.com/java-threadlocal#threadlocalsand-thread-pools)
-------------------------------------------------------------------------------------------------------------

*ThreadLocal* provides an easy-to-use API to confine some values to each thread. This is a reasonable way of achieving [thread-safety](https://www.baeldung.com/java-thread-safety) in Java. However, we should be extra careful when we're using *ThreadLocal*s and [thread pools](https://www.baeldung.com/thread-pool-java-and-guava) together.

In order to better understand this possible caveat, let's consider the following scenario:

1.  First, the application borrows a thread from the pool.
2.  Then it stores some thread-confined values into the current thread's *ThreadLocal*.
3.  Once the current execution finishes, the application returns the borrowed thread to the pool.
4.  After a while, the application borrows the same thread to process another request.
5.  Since the application didn't perform the necessary cleanups last time, it may re-use the same *ThreadLocal* data for the new request.

This may cause surprising consequences in highly concurrent applications.

One way to solve this problem is to manually remove each *ThreadLocal* once we're done using it. Because this approach needs rigorous code reviews, it can be error-prone.

### [5.1. Extending the *ThreadPoolExecutor*](https://www.baeldung.com/java-threadlocal#1-extending-thethreadpoolexecutor)

As it turns out, it's possible to extend the *ThreadPoolExecutor* class and provide a custom hook implementation for the [*beforeExecute()*](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/concurrent/ThreadPoolExecutor.html#beforeExecute(java.lang.Thread,java.lang.Runnable)) and [*afterExecute()*](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/concurrent/ThreadPoolExecutor.html#afterExecute(java.lang.Runnable,java.lang.Throwable)) methods. The thread pool will call the *beforeExecute()* method before running anything using the borrowed thread. On the other hand, it'll call the *afterExecute()* method after executing our logic.

Therefore, we can extend the *ThreadPoolExecutor* class and remove the *ThreadLocal* data in the *afterExecute()* method:

```
public class ThreadLocalAwareThreadPool extends ThreadPoolExecutor {

    @Override
    protected void afterExecute(Runnable r, Throwable t) {
        // Call remove on each ThreadLocal
    }
}
```

If we submit our requests to this implementation of *[ExecutorService](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/concurrent/ExecutorService.html)*, then we can be sure that using *ThreadLocal* and thread pools won't introduce safety hazards for our application.

6\. [Conclusion](https://www.baeldung.com/java-threadlocal#conclusion)
----------------------------------------------------------------------

In this brief article, we examined the *ThreadLocal *construct. We implemented the logic that uses *ConcurrentHashMap *that was shared between threads to store the context associated with a particular *userId. *Then we rewrote our example to leverage *ThreadLocal *to store data associated with a particular *userId* and a particular thread.

The code backing this article is available on GitHub. Once you're logged in as a [Baeldung Pro Member](https://www.baeldung.com/members/), start learning and coding on the project.

-------
Handling concurrency in an application can be a tricky process with many potential pitfalls. A solid grasp of the fundamentals will go a long way to help minimize these issues.

Get started with understanding multi-threaded applications with our Java Concurrency guide:

[>> Download the eBook](https://www.baeldung.com/eBook-java-concurrency-NPI-2-tGF65)