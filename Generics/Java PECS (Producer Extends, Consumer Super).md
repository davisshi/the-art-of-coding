In Java generics, PECS (Producer Extends, Consumer Super) is a mnemonic for managing type variance with wildcards, addressing the limitations of Java's default invariance. 

|  Term | Concept             | Wildcard  | Variance Type  |
|-------|---------------------|---|---|
| Invariance | Exact match required | None  | Invariant  |
| Producer Extends | Read |<? extends T>|Covariant|
| Consumer Super | Write |<? super T>|Contravariant|


1\. Invariance (Default Behavior) 

By default, Java generics are invariant. This means that even if `String` is a subtype of `Object`, a `List<String>` is not considered a subtype of `List<Object>`. 

java

```
List<String> strings = new ArrayList<>();
// List<Object> objects = strings; // Compilation Error: Incompatible types

```

Use code with caution.

This ensures type safety. If the above assignment were allowed, you could add an `Integer` to `objects`, which would break the original `strings` list. 

2\. Covariance (`? extends T`)

"Producer Extends" (PECS) 

Use the `<? extends T>` wildcard when your generic container acts primarily as a producer of `T` instances (you are reading data *from* it). This introduces covariance, allowing you to use a more specific type than `T`. 

-   Rule: If you only call `get()` methods, use `extends`.
-   Example: `List<? extends Number> producers = new ArrayList<Integer>();`
-   Behavior: You can read items out as `Number` (or `Object`), but you cannot `add` any elements (except `null`) because the compiler can't guarantee the exact subtype at runtime (it might be a `List<Double>`). 

3\. Contravariance (`? super T`)

"Consumer Super" (PECS)

Use the `<? super T>` wildcard when your generic container acts primarily as a consumer of `T` instances (you are writing data *into* it). This introduces contravariance, allowing you to use a more general (super) type than `T`. 

-   Rule: If you only call `add()` methods, use `super`.
-   Example: `List<? super Cat> consumers = new ArrayList<Animal>();`
-   Behavior: You can `add` any `Cat` or subtype of `Cat` (like `SiameseCat`) to the list. You can only retrieve items as `Object` (the common supertype of `Animal` and `Cat`), so reading requires casting.