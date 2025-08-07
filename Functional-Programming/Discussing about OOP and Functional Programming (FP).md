## Discussing about OOP and Functional Programming (FP)

I think this article author's thought is not correct, and even a chaos.

OOP is still having its benefits. When there are many things with specific operations required from business domain, then it is better to use OOP to define different objects with features of encapsulation, abstraction, inheritance, and polymorphism to reuse code effectively.

This article said that OOP causes lots of unnecessary inheritance, and therefore, causes the limitation of the polymorphism. This is absolutely wrong. If there is any unnecessary inheritance existing, then that only means that the interface, base class, parent class, and abstract class designed and created by developer is wrong. The developer should obey the Interface Segregation Principle to make sure that a client should never be forced to implement an interface that it doesn't use, or a client shouldn't be forced to depend on methods they do not use.

Actually OOP inheritance is the important factor to realize the polymorphism by override. And OOP class' overload also realize the polymorphism.

Therefore, saying that OOP inheritance limits the polymorphism is definitely not correct, and it is ridiculously wrong.

And for the module decoupling purpose for flexibilities, developer need to obey the Dependency Inversion Principle. All the high-level module must not depend on the low-level module, but they both should depend on abstractions.

And this article also mentions the immutable struct and protocol/trait. And saying that protocol/trait can make objects realizing more flexibilities. This is a wrong concept. To make objects realizing more flexibilities is more depending on how to design and define the objects, not just depending on which feature is used, like trait. OOP could utilize lots of different design patterns to make the objects realizing the flexibilities easily. And inheritance definitely is not a factor to block or decrease the polymorphism and flexibilities.

Actually this immutable struct and protocol/trait is related to functional programming. Functional programming has its benefits when it is used in the scenario that there are few or fixed things with more operations. Therefore, functional programming is good for adding more functions without changing any other logic in the program. Functional Programming uses pure functions which don't allow manipulate the status, therefore, that's no side effects. Since there is no status modified and no side effects, functional programming natively support parallel/concurrent programming without locks, which OOP has to use. And it is true that compiler could compile and optimize functional programming code more easier than OOP code.

Conclusion: this article's author misunderstood the OOP and its inheritance. OOP still is very useful to design different objects for domain models with features of encapsulation, abstraction, inheritance, and polymorphism.

And the author even doesn't realize what he talks about immutable struct and protocol/trait is related to Functional Programming(FP). Both OOP and Functional Programming are important for designing and developing the software projects. Both have their own pros and cons. OOP is imperative programming, it is easier to realize, but hard to maintain because of lots of different level objects and inheritance. FP is declarative programming, code is more concise but it is hard to understand if the developer has no correct FP concepts. And OOP and FP are different programming paradigms, both have their own advantages and their own applying scenarios. Therefore, all modern programming languages, like Java, Scala, C#, Python, support both OOP and FP.

At last I appreciate that the author uses the example for the relationship between OOP inheritance and the history inheritance of China. However, OOP inheritance is not just inherited all the features from parent class. If it is not suitable, then the child could modify it by overriding, and if not useful anymore, then could redesign this child class and inherit only the useful part of features and create new useful features for its own, just like in the Chinese history, we inherit the good tradition, we modify the unsuitable tradition, and we totally discard the bad tradition, and innovate the new awesome tradition nowadays, just like the OOP inheritance does.