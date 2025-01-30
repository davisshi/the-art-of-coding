[The return Keyword in Scala](https://www.baeldung.com/scala/return-keyword)
===========================

Last updated: March 18, 2024

![](https://secure.gravatar.com/avatar/039246dfabfec1c95fdacfe314fe295f?s=50&r=g)

Written by:[Samuel Orji](https://www.baeldung.com/scala/author/awesomeorji "Posts by Samuel Orji")

![](https://secure.gravatar.com/avatar/629fdde67cb23f9d3799635d89c7b250?s=50&r=g)

Reviewed by:[Grzegorz Piwowarek](https://www.baeldung.com/scala/editor/grzegorz-author "Reviewed by Grzegorz Piwowarek")

-   [Scala Syntax](https://www.baeldung.com/scala/category/syntax)

[1\. Overview](https://www.baeldung.com/scala/return-keyword#overview)
----------------------------------------------------------------------

In this tutorial, we'll explain the *return* keyword in Scala.

The Scala programming language, much like Java, has the *return* keyword, but its use is highly discouraged as it can easily change the meaning of a program and make code hard to reason about.

[2\. Introduction](https://www.baeldung.com/scala/return-keyword#introduction)
------------------------------------------------------------------------------

In Java, the *return* keyword is mandatory and is used to complete the execution of a method:

```
public boolean isEven(int number){
   return number % 2 == 0;
}
```

We can also use the *return* keyword in Scala:

```
private def isEven(number : Int) : Boolean = {
    return number % 2 == 0
}
```

But in Scala, the *return* keyword is optional, as the Scala compiler treats the value of the last execution within a function as the return value so that we can rewrite our function:

```
private def isEven(number : Int) : Boolean = {
   number % 2 == 0
}
```

Now, why are we discouraged from using the *return* keyword in Scala if it behaves the same way as in Java and has the same semantics?

### [3\. Referential Transparency](https://www.baeldung.com/scala/return-keyword#referential-transparency)

A piece of code is defined as referentially transparent if we can safely replace that piece of code with the value it computes and vice-versa, anywhere where that piece is used, without changing the meaning or result of our program. 

If the *return* keyword is referentially transparent, then we should replace the expression that uses the *return* keyword with its value:

```
private def isPositiveNumber1(number : Int ) : Boolean = {
   val isTrue = return true
   val isFalse = return false

   if(number > 0) isTrue else isFalse
}

private def isPositiveNumber2(number : Int ) : Boolean = {
  if(number > 0) return true else return false
}

println(isPositiveNumber1(-1)) // true
println(isPositiveNumber2(-1)) // false
```
We can see in our example that by replacing a value with its computation using the *return* keyword, some inconsistencies arise. The entire program changes, which breaks referential transparency.

Now, let's see what happens when we don't use the *return* keyword:

```
private def isPositiveNumber1(number : Int ) : Boolean = {
   val isTrue = true
   val isFalse = false

   if(number > 0) isTrue else isFalse
}

private def isPositiveNumber2(number : Int ) : Boolean = {
  if(number > 0) true else false
}

println(isPositiveNumber1(-1)) // false
println(isPositiveNumber2(-1)) // false
```

We see that our program didn't change, which means we maintained referential transparency.

The *return* keyword isn't referentially transparent because the *return* keyword or expression, when evaluated, abandons the current computation and returns to the caller of the method in which *return* appears.

[4\. Inlining](https://www.baeldung.com/scala/return-keyword#inlining)
----------------------------------------------------------------------

[Inlining](https://www.baeldung.com/scala/inline-noinline-annotations) refers to replacing a function call with its body or definition.

Let's see how using the *return* keyword causes inconsistencies when inlining a function. First, we define a function that uses the *return *keyword, and see if it gives us our desired result:

```
def multiplier(a : Int, b: Int) : Int = return a * b
val randomNumbers = List(1,2,3,4)
def multiple(numbers : List[Int]) : Int = {
    numbers.foldLeft(1)(multiplier)
}
println(multiple(randomNumbers)) // 24
```

This works as expected. Now, what happens when we inline the *multiplier* function by replacing the function with its content:

```
val randomNumbers = List(1,2,3,4)
def multiple(numbers : List[Int]) : Int = {
  numbers.foldLeft(1){(a,b) => return a * b}
}
println(multiple(randomNumbers)) // 1 ??

```
We get the wrong result. This is because the *return* keyword abandons the current computation and returns whatever was passed to it at the time it was evaluated, which in the case of our *foldLeft *is 1.

[5\. Early *return*](https://www.baeldung.com/scala/return-keyword#early-return)
--------------------------------------------------------------------------------

We may be wondering how we can implement early returns if we aren't supposed to use the *return *keyword. This is where we're advised to use other mechanisms such as recursion.

Let's see how we could write our version of *indexOf *in Java if it wasn't already a method on the *String* class:

```
int indexOf(String string, char character){
    if(string.isEmpty()) {
        return -1;
    } else {
        int index = -1;
        int i;
        char[] stringArray = string.toCharArray();
        for(i= 0; i <= string.length() - 1; i++){
            if (stringArray[i] == character)
                return i;
        }
        return index;
    }
}
```

We return early when we find the index. How do we do this in Scala if we aren't supposed to use the *return* keyword to break out of a loop?

This is where we can use functional programming methods such as recursion, which makes our code easier to understand:

```
def indexOf(string : String , char : Char) : Int = {
   def runner(stringList : List[Char], index : Int) : Int = {
     stringList match {
       case Nil => -1
       case h :: _ if h == char => index + 1
       case _ :: t => runner(t , index + 1)
     }
   }
   if(string.isEmpty) -1 else runner(string.toList, -1)
}
println(indexOf("hello",'h') // 0
println(indexOf("hello",'z') // -1
```

There's no *return* keyword insight, and our program works just fine.

[6\. Conclusion](https://www.baeldung.com/scala/return-keyword#conclusion)
--------------------------------------------------------------------------

In this article, we've seen how the *return* keyword in Scala shares similarities with its Java counterpart and why it's not advisable to use the keyword as it breaks referential transparency. We may think that there may be a use case for using the *return* keyword in Scala, but there's really none.

As usual, the source code can be found [over on GitHub](https://github.com/Baeldung/scala-tutorials/tree/master/scala-core-modules/scala-core-7).