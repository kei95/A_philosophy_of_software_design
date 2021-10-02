# Chapter 18

## Code Should be Obvious
 > Obscurity is one of the two main causes of complexity described in Section 2.3, which are *dependencies* and *obscurity*. Obscurity occurs when important information about a system is not obvious to new developers.
 - The solution to the obscurity problem is to write code in a way that makes it obvious; this chapter discuss some of the factors that make code more or less obvious.

 > If code is obvious, it means that someone can read the code quickly, without much thought, and their first guesses about the behavior or meaning of the code will be correct.
 - If code is obvious, reader doesn't need to spend much time or effort to gather all the information they need to work with the code.
 - If code is not obvious, then a reader must expand a lot of time  and evergy to understand it.
   - Not only does this reduce their efficiency, but it also increases the likelihood of misunderstanding and bugs. Obvious code needs fewer comments than non-obvious code.

 > "Obvious" is in the mind of the reader: it's easier to notice that someone else's code is non-obvious than to see problems with your own code. Thus, the best way to determine the obviousness of code is through code reviews. 
 - If someone reading your code says it's not obvious, then it's not obvious, no matter how clear it may seem to you.
 - By trying to understand what made the code non-obvious, you'll learn how to write better code in the future.

 ## 18.1 Things that make code more obvious
 > Two of the most important techniques for making code obvious have already been discussed in previous chapters.
 - The first is choosing good names[Chapter 14](https://github.com/kei95/A_philosophy_of_software_design/blob/master/Chapter14.md#chapter-14). Precise and meaningful names clarify the behavior of the code and reduce the need for documentation. if a name is vague or ambiguous, then readers will have read through the code in order to deduce the meaning of the named entity; this is time-consuming and error-prone.
 - The second technique is consistency [Chapter 17](https://github.com/kei95/A_philosophy_of_software_design/blob/master/Chapter17.md#chapter-17). If similar things are always done in similar ways, then readers can recognize patterns they have seen before and immediately draw(safe) conclusions without analyzing the code in detail.
 - Here are a few other general-purpose techniques for making code more obvious:
 ### Judicious use of white space
 - The way code is formatted can impact how easy it is to understand. Even in a comment, aligning comments with white spaces makes it easier to read for other developers.

### Comments
 - Sometimes it isn't possible to avoid code that is non-obvious. When this happens, it's important to use comments to compensate by providing the missing information. TO do this well, you must put yourself in the position of the reader and figure out what is likely to confuse them, and what information will clear up that confusion. The next section shows a few examples.

 ## Things that make code less obvious
 > There're many things that can make code non-obvious; this section provides a few examples. Some of these, such as event-driven programing, are useful in some situations, so you may end up using them anyway. When this happens, extra documentation can help to minimize reader confusion.

 ### Event-driven programing
 > In event-driven programming, an application responds to external occurrences, such as the arrival of a network packet or the press of a mouse button. One module is responsible for reporting incoming events. Other parts of the application register interest in certain events by asking the event module to invoke a given function or method when those events occur.
 - Event-driven programming makes it hard to follow the flow of control. The event handler functions are never invoked directly; they are invoked indirectly by the event module, typically using a function pointer or interface.
 - Even if you find the point of invocation in the event module, it still isn't possible to tell which specific function will be invoked: this will depend on which handlers were registered at runtime. Because of this, it's hard to reason about event-driven code or convince yourself that it works.

## RED FLAT: Non-obvious code
 - If the meaning and behavior of code cannot be understood with a quick reading, it's a red flag. Often this means that there's important information that is not immediately clear to someone reading the code.

 ### Generic containers
 > Many languages provide generic classes for grouping two or more items into a single object, such as *Pair* in Java. These classes are tempting because they make it easy to pass around several objects with a single variable.
 - One of the most common uses is to return multiple values from a method, as in this Java example:
 ```
 return new Pair<Integer, Boolean>(currentTerm, false);
 ```
  - Unfortunately, generic containers result in non-obvious code because the grouped elements have generic names that obscure their meaning.
  - In the example above, the caller must reference the two return values with `result.getKey()` and `result.getValue()`, which give no clue about the actual meaning of the values. Thus, it's better not to use generic containers.
  - If you need a container, define a new class or structure that is specialized for the particular use. You can then use meaningful names for the elements, and you can provide additional documentation in the declaration, which is not possible with the generic container.

 > This example illustrates a general rule: **software should be designed for ease of reading, not ease of writing**. Generic containers are expedient for the person writing the code, but they create confusion for all the readers that follow. It's better for the person writing the code to spend a few extra minutes to define a specific container structure, so that resulting code is more obvious.

 ### Different types for declaration and allocation.
 - Consider the following Java example:
 ```
 private List<Message> incomingMessageList; 
 ...
 incomingMessageList = new ArrayList<Message>();
 ```
 - The variable is declared as a `List`, but the actual value is an `ArrayList`. This code is legal, since `List`is a superclass of `ArrayList`, but it can mislead a reader who sees the declaration but not the actual allocation. 
 - The actual type may impact how the variable is used (`ArrayList` have different performance and thread-safety properties than other subclasses of `List`), so it's better to match the declaration with the allocation.

 ### Code that violates reader expectations.
 > Consider the following code, which is the main program for a Java app.
 ```
 public static void main(String[] args) 
 { 
     ... 
     new RaftClient(myAddress, serverAddresses); 
}
 ```
 - Most application exit when their main programs return, so readers are likely to assume that will happen here. However, that is not the case.
 - The constructor for `RaftClient`creates additional threads, which continue to operate even though the application's main thread finishes.
   - This behavior should be documented in the interface comment for the `RaftClient` constructor, but the behavior is non-obvious enough that it's worth putting a short comment at the end of `main` as well.
   - The comment should indicate that the application will continue executing in other threads. Code is most obvious if it conforms to the conventions that readers will be expecting; if it doesn't, then it's important to document the behavior so readers aren't confused.

 ## Conclusion
 > Another way of thinking about obviousness is in terms of information. If code is non-obvious, that usually means there's important information about the code that the reader doesn't have:
  - in the `RaftClient` example, the reader might not know that the `RaftClient` constructor created new threads; in the `Pair` example, the reader might not know that `result.getKey()` returns the number of the current term.
  - To make code obvious, you must ensure that readers always have the information they need to understand it.
  - The best way is to reduce the amount of information that is needed, using design techniques such as abstraction and elimination special cases.
    - Second, you can take advantage of information that readers have already acquired in other contexts(for example, by following conventions and conforming to expectations) so readers don't have to learn new information for your code.
    - Third, you can present the important information to them in the code, using techniques such as good names and strategic comments.