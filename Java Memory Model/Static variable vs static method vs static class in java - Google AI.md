Static variable vs. static method vs. static class in Java

![Understanding Static and Instance Variables in Java | by ...](http://t3.gstatic.com/images?q=tbn:ANd9GcQ6m7SgXObpxiCKqtdWCjlHGQH3WKn1BNxQvMwDNh8G1C4tq5G1LylGFKpvJWgjHRNcalzLqtfW)

![Static Method in Java With Examples - GeeksforGeeks](http://t1.gstatic.com/images?q=tbn:ANd9GcQauXiar0yJGP-5VFKI8bcOT-AKShs1D1jg04qrr-A0FHyD8c6zINtvfVrIT50B2xBJNWD2_G2k)

![Should you avoid using static? | AT&T Israel Tech Blog](http://t3.gstatic.com/images?q=tbn:ANd9GcTTX13j8Wocgue3FoEfb21ufdSC4cWHUlivl4tEW8DDKKqUHPwr_vZ1DKIznPdK1FtSxF9OD1OU)

![Static in Java: An Overview of Static Keyword in Java With ...](http://t0.gstatic.com/images?q=tbn:ANd9GcTQWRRsFtr2CI4My3mg2zZkVdZCFd2MPoM1tMrVDPSixl7yBu_DRiRwM2nBfWRZmU13RybkUUeU)

![Difference between static methods, static variables, and ...](http://t0.gstatic.com/images?q=tbn:ANd9GcQl-A-nQq5TPV0BqObmKp5NFZx59M9wFwZ_9iOWhiNr2NcNYSAnwBiiQuPvdN1PdUolwRpXGsJS)

In Java, the `static` keyword modifies how members (variables, methods, and nested classes) are associated with a class or its instances. 

Here's a breakdown:

1\. Static variables (class variables)

-   Definition: A variable declared with the `static` keyword.
-   Belongs to: The class itself, not individual objects.
-   Memory: One copy of the static variable is created when the class is loaded, and it's shared among all objects of that class. This makes it memory-efficient compared to instance variables.
-   Access: Can be accessed using the class name directly, e.g., `ClassName.staticVariable`.
-   Use cases:
    -   Representing properties common to all instances of a class, such as a company name for all employees.
    -   Counting the number of objects created for a class.
    -   Storing constant values that remain unchanged throughout the program's execution. 

2\. Static methods (class methods)

-   Definition: A method declared with the `static` keyword.
-   Belongs to: The class itself, not an object.
-   Memory: Stored in a dedicated area of memory when the class is loaded and persists as long as the class is in use.
-   Access: Invoked directly using the class name, e.g., `ClassName.staticMethod()`.
-   Restrictions:
    -   Can only directly call other static methods and access static variables.
    -   Cannot access non-static (instance) variables or methods directly because they don't operate on any specific instance.
    -   Cannot use the `this` or `super` keywords.
-   Use cases:
    -   Utility or helper functions that don't depend on the object's state, like mathematical operations in the `Math` class or string manipulations in a `StringUtils` class.
    -   Methods that operate on static variables, such as modifying a shared counter.
    -   Providing factory methods to create instances of a class.
    -   Serving as the entry point for a Java application (e.g., `public static void main(String[] args)`). 

3\. Static classes (static nested classes)

-   Definition: A class declared with the `static` keyword, but only applicable to nested classes (classes defined inside another class).
-   Belongs to: The outer class, but its instances are independent of the outer class's instances.
-   Memory: Does not require an instance of the outer class to be created, and consumes less memory compared to non-static inner classes.
-   Access: Can access only the static members (variables and methods) of the outer class.
-   Note: Top-level classes cannot be declared as `static`.
-   Use cases:
    -   Grouping related utility methods or constants within a class for better code organization and readability.
    -   Encapsulating helper methods or functionality closely related to the outer class but not dependent on its instance.
    -   Implementing design patterns like Singleton, where a single instance of the class is required. 

In essence

-   Static variables store data shared across all instances of a class.
-   Static methods encapsulate behavior associated with the class itself, usable without creating an object.
-   Static classes (nested) provide a way to group related classes or functionalities within an outer class without depending on its instances.