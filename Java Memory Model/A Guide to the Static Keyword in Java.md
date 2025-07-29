[A Guide to the Static Keyword in Java](https://www.baeldung.com/java-static)
=====================================

Last updated: January 8, 2024

![](https://secure.gravatar.com/avatar/f7bfa7ac878afa29edaf04960cdc924cd1d8228a4dbc84dbd410e20fb76b2e4c?s=50&r=g)

Written by:[baeldung](https://www.baeldung.com/author/baeldung "Posts by baeldung")

![](https://secure.gravatar.com/avatar/c297fbf3300f55f1f8bd55cec61adeea600aec6e79d461acfc2306be0e58c853?s=50&r=g)

Reviewed by:[Michal Aibin](https://www.baeldung.com/editor/michal-author "Reviewed by Michal Aibin")

-   [Core Java](https://www.baeldung.com/category/java/core-java)

-   [Definition](https://www.baeldung.com/tag/definition)

-   [Java Keyword](https://www.baeldung.com/tag/java-keyword)

1\. [Overview](https://www.baeldung.com/java-static#overview)
-------------------------------------------------------------

In this tutorial, we'll explore the *static* keyword of the Java language in detail. The *static* keyword means that a member -- like a field or method -- belongs to the class itself, rather than to any specific instance of that class. As a result, we can access static members without the need to create an instance of an object.

We'll begin by discussing the differences between static and non-static fields and methods. Then, we'll cover static classes and code blocks, and explain why non-static components can't be accessed from a static context.

2\. [The *static* Fields (Or Class Variables)](https://www.baeldung.com/java-static#static-fields)
--------------------------------------------------------------------------------------------------

In Java, when we declare a field *static*, exactly a single copy of that field is created and shared among all instances of that class.

It doesn't matter how many times we instantiate a class. There will always be only one copy of *static* field belonging to it. The value of this *static* field is shared across all objects of the same class. From the memory perspective, static variables are stored in the heap memory.

Imagine a class with several instance variables, where each new object created from this class has its own copy of these variables. However, if we want a variable to track the number of objects created we use a static variable instead. This allows the counter to be incremented with each new object:

```
public class Car {
    private String name;
    private String engine;

    public static int numberOfCars;

    public Car(String name, String engine) {
        this.name = name;
        this.engine = engine;
        numberOfCars++;
    }

    // getters and setters
}
```

As a result, the static variable *numberOfCars *will be incremented each time we instantiate the *Car *class. Let's create two *Car *objects and expect the counter to have a value of two:

```
@Test
public void whenNumberOfCarObjectsInitialized_thenStaticCounterIncreases() {
    new Car("Jaguar", "V8");
    new Car("Bugatti", "W16");

    assertEquals(2, Car.numberOfCars);
}
```

As we can see *static *fields can come in handy when:

-   the value of the variable is independent of objects
-   the value is supposed to be shared across all objects

Lastly, it's important to know that static fields can be accessed through an instance (e.g. *ford.numberOfCars++*) or directly from the class (e.g. *Car.numberOfCars++*). The latter is preferred, as it clearly indicates that it's a class variable rather than an instance variable.

3\. [The *static* Methods (Or Class Methods)](https://www.baeldung.com/java-static#static-methods)
--------------------------------------------------------------------------------------------------

Similar to *static* fields, *static* methods also belong to a class instead of an object. So, we can invoke them without instantiating the class. Generally, we use *static* methods to perform an operation that's not dependent upon instance creation.

For example, we can use a *static* method to share code across all instances of that class:

```
static void setNumberOfCars(int numberOfCars) {
    Car.numberOfCars = numberOfCars;
}
```

Additionally, we can use *static* methods to create utility or helper classes. Some popular examples are the JDK's [*Collections*](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Collections.html) or [*Math*](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Math.html) utility classes, Apache's [*StringUtils,*](https://commons.apache.org/proper/commons-lang/apidocs/org/apache/commons/lang3/StringUtils.html) and Spring Framework's [*CollectionUtils*](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/util/CollectionUtils.html).

The same as for *static* fields, *static* methods can't be overridden. This is because *static* methods in Java are resolved at compile time, while method overriding is part of Runtime Polymorphism.

The following combinations of the instance, class methods, and variables are valid:

1.  instance methods can directly access both instance methods and instance variables
2.  instance methods can also access *static* variables and *static* methods directly
3.  *static* methods can access all *static* variables and other *static* methods
4.  *static* methods can't access instance variables and instance methods directly. They need some object reference to do so.

4\. [The *static* Code Blocks](https://www.baeldung.com/java-static#static-code-blocks)
---------------------------------------------------------------------------------------

Generally, we'll initialize *static* variables directly during declaration. However, if the *static* variables require multi-statement logic during initialization we can use a *static* block instead.

For instance, let's initialize a *List* object with some predefined values using *static* block of code:

```
public class StaticBlockDemo {
    public static List<String> ranks = new LinkedList<>();

    static {
        ranks.add("Lieutenant");
        ranks.add("Captain");
        ranks.add("Major");
    }

    static {
        ranks.add("Colonel");
        ranks.add("General");
    }
}
```

As we can see, it wouldn't be possible to initialize a *List* object with all the initial values along with the declaration. So, this is why we've utilized the *static* block here.

A class can have multiple *static* members. The JVM will resolve the *static* fields and *static* blocks in the order of their declaration. To summarize, the main reasons for using *static *blocks are:

-   to initialize *static *variables needs some additional logic apart from the assignment
-   to initialize *static* variables with a custom exception handling

5\. [The *static* Inner Classes](https://www.baeldung.com/java-static#static-inner-classes)
-------------------------------------------------------------------------------------------

Java allows us to create a class within a class. It provides a way of grouping elements we use in a single place. This helps to keep our code more organized and readable.

In general, the nested class architecture is divided into two types:

-   nested classes that we declare *static* are called *static* nested classes
-   nested classes that are non-*static* are called inner classes

The main difference between these two is that the inner classes have access to all members of the enclosing class (including *private *ones), whereas the *static *nested classes only have access to static members of the outer class.

*Static* nested classes behave exactly like any other top-level class -- but are enclosed in the only class that will access it, to provide better packaging convenience.

For example, we can use a nested static class to implement the [singleton pattern](https://www.baeldung.com/java-singleton):

```
public class Singleton  {
    private Singleton() {}

    private static class SingletonHolder {
        public static final Singleton instance = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHolder.instance;
    }
}
```

We use this method because it doesn't require any synchronization and is easy to learn and implement.

Additionally, we can use a nested *static class *where visibility between parent and nested members is displayed, and vice versa:

```
public class Pizza {

    private static String cookedCount;
    private boolean isThinCrust;

    public static class PizzaSalesCounter {

        private static String orderedCount;
        public static String deliveredCount;

        PizzaSalesCounter() {
            System.out.println("Static field of enclosing class is "
              + Pizza.cookedCount);
            System.out.println("Non-static field of enclosing class is "
              + new Pizza().isThinCrust);
        }
    }

    Pizza() {
        System.out.println("Non private static field of static class is "
          + PizzaSalesCounter.deliveredCount);
        System.out.println("Private static field of static class is "
          + PizzaSalesCounter.orderedCount);
    }

    public static void main(String[] a) {
           new Pizza.PizzaSalesCounter();
    }
}
```

The result when we run the main method is:

```
Static field of enclosing class is null
Non private static field of static class is null
Private static field of static class is null
Non-static field of enclosing class is false
```

Basically, a *static* nested class doesn't have access to any instance members of the enclosing outer class. It can only access them through an object's reference. The main reasons for using *static *inner classes in our code are:

-   grouping classes intended for use in only one place increases encapsulation.
-   to bring the code closer to the only place that will use it. This increases readability, and the code is more maintainable.
-   if a nested class doesn't require any access to its enclosing class instance members, it's better to declare it as *static*. This way, we won't couple it to the outer class, and they won't require any heap or stack memory.

6\. [Understanding the *"Non-static variable"* Error](https://www.baeldung.com/java-static#non-static-variable-from-static-context)
-----------------------------------------------------------------------------------------------------------------------------------

The error *"Non-static variable cannot be referenced from a static context"* occurs when a non-static variable is used inside a static context. As we saw earlier, the JVM loads static variables at class load time, and they belong to the class. On the other hand, we need to create an object to refer to non-static variables.

So, the Java compiler complains because there's a need for an object to call or use non-static variables.

Now that we know what causes the error, let's illustrate it using an example:

```
public class MyClass {
    int instanceVariable = 0;

    public static void staticMethod() {
        System.out.println(instanceVariable);
    }

    public static void main(String[] args) {
        MyClass.staticMethod();
    }
}
```

As we can see, we used *instanceVariable, *which is a non-static variable, inside the static method *staticMethod(). *Consequently, we'll get the error *Non-static variable cannot be referenced from a static context.*

7\. [Conclusion](https://www.baeldung.com/java-static#conclusion)
-----------------------------------------------------------------

In this article, we saw the *static* keyword in action and discussed the main reasons for using *static* fields, methods, blocks, and inner classes.

Finally, we learned what causes the compiler to fail with the error "*Non-static variable cannot be referenced from a static context"*.

The code backing this article is available on GitHub. Once you're logged in as a [Baeldung Pro Member](https://www.baeldung.com/members/), start learning and coding on the project.