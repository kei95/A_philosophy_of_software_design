# Chapter 19

## Software trends
 > As a way of illustrating the principles discussed in this book, this chapter considers several trends and patterns that have become popular in software development over the last few decades. For each trend, I'll describe how that trend relates to the principles in this book and use the principles to evaluate whether that trend provides leverage against software complexity.

 ## 19.1 Object-oriented programming and inheritance
 > Object-oriented programming is one of the most important new ideas in software development over the last 30-40 years.
  - It introduced notions such as classes, inheritance, private methods, and instance variables.
    - If used carefully, these mechanisms can help to provide methods and variables can be used to ensure information hiding: no code outside a class can invoke private methods or access private variables, so there can't be any external dependencies on them.

 > One of the key elements of object-oriented programming is inheritance. Inheritance comes in two forms, which have different implications for software complexity. 
 ### First form - interface inheritance
 - The first form of inheritance is interface inheritance, in which a parent class defines the signatures for one or more methods, but doesn't implement the methods.
   - Each subclass must implement the signatures, but different subclasses can implement the same methods in different ways.
     - For example, the interface might define methods for performing I/O; one subclass might implement the I/O operations for disk files, and another subclass might implement the same operations for network sockets.
 - Interface inheritance provides leverage against complexity by reusing the same interface for multiple purposes. It allows knowledge acquired in solving one problem to be used to solve other problems. Another way of thinking about this is in terms of depth: the more different implementations there are of an interface, the deeper the interface becomes.
 - In order for an interface to have many implementations, it must capture the essential features of all the underlying implementations while steering clear of the details that differ between the implementations; the notion is at the heart of abstraction.

 ### Second form - implementations inheritance
 - The second form of inheritance is implementation inheritance. In this form, a parent class defined not only signatures for one or more methods, but also default implementations. Subclasses can choose to inherit the parents's implementation of a method or override it by defining a new method with the same signature.
   - Without implementation inheritance, the same method implementation might need to be duplicated in several subclasses, which would create dependencies between those subclasses(modifications would need to be duplicated in all copies of the method). Thus, implementation inheritance reduces the amount of code that needs to be modified as the system evolves; in other words, it reduces the change amplifications problem.
 - However, implementation inheritance creates dependencies between the parent class and each of its subclasses. Class instance variables in the parent class are often accessed by both the parent and child classes; this results in information leakage between the classes in the inheritance hierarchy and makes it hard to modify one class in the hierarchy without looking at the others.
   - In the worst case, programmers will need complete knowledge of the entire class hierarchy underneath the parent class in order to make changes to any of the classes.
     - Class hierarchies that use implementation inheritance extensively tend to have high complexity. Thus, implementation inheritance should be used with caution. Before using implementation inheritance, consider whether an approach based on *composition* can provide the same benefits.
       - For example, it may be possible to use small helper classes to implement the shared functionality. Rathe than inheriting functions from a parent, the original classes can each build upon the features of the helper classes.
       - If there's no viable alternative to implementation inheritance, try to separate the state managed by the parent class from that managed by subclasses. Onc way to do this is for certain instance variables to be managed entirely by methods in the parent class, with subclasses using them only in a read-only fashion or through other methods in the parent class. This applies the notion of information hiding within the class hierarchy to reduce dependencies.
 - Although the mechanisms provided by object-oriented programming can assist in implementing clean designs, they do not, by themselves, guarantee good design. For example, if classes are shallow, or have complex interfaces, or permit external access to their internal state, then they will still result in high complexity.

 ## 19.2 Agile development
 > Agile development is an approach to software development that emerged in the late 1990's from a collection of ideas about how to make software development more lightweight, flexible, and incremental; it was formally defined during a meeting of practitioners in 2001. Agile development is mostly about the process of software development(organizing teams, meaning schedules, the role of unit testing, interacting with customers, etc.) as opposed to software design. Nonetheless, it relates to some of the design principles in this book.
 - One of the most important elements of agile development is the notion that development should be incremental and iterative. In the agile approach, a software system is developed in a series of iterations, each of which adds and evaluates a few new features; each iteration includes design, test, and customer support.
 - In general this is similar to the incremental approach advocated here. As mentioned in Chapter 1, it isn't possible to visualized a complex system well enough at the outset of a project to determine the best design.
 - The best way to end up with a good design is to develop a system in increments, where each increment adds a few abstractions and refactors existing abstractions based on experience. This is similar to the agile development approach.
  > One of the risks of agile development is that it can lead to *tactical programming*. Agile development tends to focus developers on feature not abstractions, and it encourages developers to put off design decisions in order to produce working software as soon as possible.
  - For example, some agile practitioners argue that you shouldn't implement general-purpose right away; implement a minimal special-purpose mechanism to start with, and refactor into something more generic later, once you know that it's needed.
    - Although these arguments make sense to a degree, they argue against an investment approach, and they encourage a more tactical style of programming. This can result in a rapid accumulation of complexity.

 > Developing incrementally is generally a good idea, but **the increments of development should be abstractions, not features.** It's fine to put off all thoughts about a particular abstraction until it's needed by a feature.
 - Once you need the abstraction, invest the time to design it cleanly; follow the advice of [Chapter 6](https://github.com/kei95/A_philosophy_of_software_design/blob/master/Chapter6.md#chapter-6) and make it somewhat general-purpose.

## 19.3 Unit tests
 > If used to be that developers rarely wrote tests. If tests were written at all, they were written by a separate QA team. However, one of the tenets of agile development is that testing should be tightly integrated with developments, and programmers should write tests for their own code. This practice has now become widespread. Tests are typically divided into two kinds: unit tests and system tests.
 - Unit tests are the onces most often written by developers. They are small and focused: each test usually validates a small section of code in a single method. Unit tests can be run in isolation, without setting up a production environment for the system. 
 - Unit tests are often run in conjunction with a test coverage tool to ensure that every line of code in the application is tested. Whenever developers write new code or modify existing code, they are responsible for updating the unit tests to maintain proper test coverage.

 > The second kind of test consists of system tests(sometimes called integration tests), which ensure that the different parts of an application all work together properly. They typically involve running the entire application in a production environment. System tests are more likely to be written by a separate QA or testing team.
 - Tests, particularly unit tests, play an important role in software design because they facilitate refactoring. Without a test suite, it's dangerous to make major structural changes to a system. There's no easy way to find bugs, so it's likely that bugs will go undetected until the new code is deployed, where they are much more expensive to find and fix.
 - As a result, developers avoid refactoring in systems without good test suites; they try to minimize the number of code changes for each new feature or bug fix, which means that complexity accumulates and design mistakes don't get corrected.

 > With a good set of tests, developers can be more confident when refactoring because the test suite will find most bugs that are introduced. This encourages developers to make structural improvements to a system, which results in a better design. Unit tests are particularly valuable: they provide a higher degree of code coverage than system tests, so they are more likely to uncover any bugs.
 - For example during the development of the Tcl scripting language, we decided to improve performance by replacing Tcl's interpreter with a byte-code compiler. This was a huge change that affected almost every part of the core Tcl engine. Fortunately, Tcl had an excellent unit test suite, which we ran on the new byte-code engine. The existing tests were so effective in uncovering bugs in the new engine that only a single bug turned up after the alpha release of the byte-code compiler.

 ## Test-driven development
 > Test-driven development is an approach to software development where programmers write unit tests before they write code. When create a new class, the developer first writes unit tests for the class based on its expected behavior. None of the tests pass, since there's no code for the class. Then the developer works through the tests one at a time, writing enough code for that test to pass. When all of the tests pass, the class is finished.
 - Although the arthur is a strong advocate of unit testing, he's not a fan of TDD. **The problem with TDD is that it focuses attention on getting specific features working, rather than finding the best design**
   - This is tactical programming pure and simple, with all of its disadvantages. TDD is too incremental: at any point in time, it's tempting to just hack in the next feature to make the next test pass. There's no obvious time to design, so it's easy to end up with a mess.
 - The units of development should be abstractions, not features. Once you discover the need for an abstraction, don't create the abstraction in pieces over time; design it all at once.
   - This is more likely to produce a clean design whose pieces fit together well.
 - One place where it makes sense to write the tests first is when fixing bugs. Before fixing a bug, write a unit test that fails because of the bug. Then fix the bug and make sure that the unit test now passes.
   - This is the best way to make sure you really have fixed the bug. If you fix the bug before writing the test, it's possible that the new unit test doesn't actually trigger the bug, in which case it won't tell you whether you really fixed the problem.

 ## Design patterns
 > A design patterns is a commonly used approach for solving a particular kind of problem, such as an iterator or an observer. The notion of design patterns was popularized by the book Design Patterns: Elements of Reusable Object-Oriented Software by Gamma, Helm, Johnson, and Vlissides, and design patterns are now widely used in object-oriented software development.
 - Design patterns represent an alternative to design: rather than designing a new mechanism form scratch, just apply a well-known design pattern.
 - The greatest risk with design patterns is over-application.
   - Not every problem can be solved with design patterns. Don't try to force a problem into a design pattern when a custom approach will be cleaner.

 ## 19.6 Getters and Setters
 > Getters and setters aren’t strictly necessary, since instance variables can be made public. The argument for getters and setters is that they allow additional functions to be performed while getting and setting, such as updating related values when a variable changes, notifying listeners of changes, or enforcing constraints on values.
 - Even if these feature aren't needed initially, they can be added later without changing the interface.
 - Although it may make sense to use getters and setters, if you must expose instance variables, it's better not to expose instance variables in the first place. Exposed instance variables mean that part of the class's implementation is visible externally, which violates the idea of information hiding and increases the complexity of the class's interface.
 - Getters and setters are shallow methods. So they clutter to the class's interface without providing much functionality. **It's better to avoid getters and setters as much as possible**

 > One of the risks of establishing a design pattern is that developers assume the patterns is good and try to use is as much as possible. This has led to over-usage of getters and setters in Java.

  ## Conclusion
  - Whenever you encounter a proposal for a new software development paradigm, challenge it from the standpoint of complexity:
    - Does the proposal really help to minimize complexity in large software systems? 
      - Many proposals sound good on the surface, but if you look more deeply you'll see that some of them make complexity worse, not better.