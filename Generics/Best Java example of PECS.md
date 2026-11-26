### [](https://)Here is a classic Java example demonstrating **PECS** (*Producer `Extends`, Consumer `Super`*) with two parameters—one acting as a **consumer** (`? super T`) and the other as a **producer** (`? extends T`):

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class PecsExample {

    /**
     * Copies matching elements from a producer list into a consumer list.
     *
     * @param dest   Consumer (? super T): accepts elements of type T (or subtypes of T).
     * @param src    Producer (? extends T): yields elements of type T (or subtypes of T).
     * @param filter Condition to decide which elements to copy.
     */
    public static <T> void copyMatching(
            List<? super T> dest,
            List<? extends T> src,
            Predicate<? super T> filter) {

        for (T item : src) {        // Reading from Producer -> safe as T
            if (filter.test(item)) {
                dest.add(item);     // Writing to Consumer -> safe to add T
            }
        }
    }

    public static void main(String[] args) {
        List<Integer> integers = List.of(1, 2, 3, 4, 5, 6);
        List<Number> numbers = new ArrayList<>();

        // T is inferred as Integer:
        // - Consumer: List<? super Integer> (satisfied by List<Number>)
        // - Producer: List<? extends Integer> (satisfied by List<Integer>)
        copyMatching(numbers, integers, n -> n % 2 == 0);

        System.out.println(numbers); // [2, 4, 6]
    }
}

```

### Why This Works

* **First parameter (`List<? super T> dest`) — Consumer:** You only *put* items into `dest`. Using `? super T` lets you pass a `List<Number>` or `List<Object>` even when `T` is `Integer`.
* **Second parameter (`List<? extends T> src`) — Producer:** You only *get* items out of `src`. Using `? extends T` lets you pass a `List<Integer>` or `List<Double>` when `T` is `Number`.
* **Bonus (`Predicate<? super T> filter`):** A `Predicate` is also a consumer of `T` (it consumes `T` to test a condition), so `? super T` makes it even more flexible—for example, a `Predicate<Number>` can filter a `List<Integer>`.

```

```

### so Consumer (? super T): accepts elements of type T or subtypes of T, correct?

**Yes, exact!** When **adding/writing** elements into a `List<? super T>`, you can safely pass an element of type `T` **or any subtype of `T**` (like `Integer` when `T` is `Integer`, or `Integer` when `T` is `Number`).

### One Important Nuance: Reading Back Out (`get`)

While you can **add** `T` and subtypes of `T` into `List<? super T>`, **reading** an element back out only guarantees type `Object`:

```java
List<? super Integer> consumer = new ArrayList<Number>();

consumer.add(10);          // OK: Integer is T
// consumer.add(new Object()); // Compile error: Object is not Integer or a subtype of Integer

Object obj = consumer.get(0); // OK: only guaranteed to be Object
// Integer i = consumer.get(0); // Compile error: could be a Number/Object at runtime

```

### Quick Cheat Sheet

* **Producer (`? extends T`)** → Safe to **read** as `T`; **cannot add** non-`null` elements (except `null`).
* **Consumer (`? super T`)** → Safe to **add** `T` and **subtypes of `T**`; **reading** only yields `Object`.
