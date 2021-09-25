# Chapter 13

## Comments Should Describe Things that Aren't Obvious from the Code
 > The reason for writing comments is that statements in a programming language can't capture all of important information that was in the mind of the developer when the code was written.
  - The guiding principle for comments is that **comments should describe things that aren't obvious form the code.**

 > There're many things that aren't obvious from the code. Sometimes it's low-level details that aren't obvious. For example, when a pair of indices describe a range, it isn't obvious whether the elements given by the indices are inside the range or not.
 - Sometimes there are rules the developer followed, such as “always invoke a before b.” You might be able to guess at a rule by looking at all of the code, but this is painful and error-prone; a comment can make the rule explicit and clear.

 > One of the most important reasons for comments is abstractions, which include a lot of information that isn't obvious from code. The idea of an abstraction is to provide a simple way of thinking about something, but code is so detailed that it can be hard to see the abstraction just from reading the code.
 - Even if this information can be deduced by the code, we don't want to force users of a module to do that: reading the code is time-consuming and forces them to consider a lot of information that isn't needed to use the module.
   - **Developers should be able to understand the abstractions provided by a module without reading any code other than its externally visible declarations**
 - Good comments typically explain things at a different level of detail than the code, which is more detailed in some situations and less detailed(more abstract) in others.

## 13.1 Pick conventions
 > The first step in writing comments is to decide on conventions for commenting, such as what you will comment and the format you will use for comments. If the language has document compilation tool, such as Javadoc for Java, follow the conventions of the tools.\
  -  Conventions serve two purposes. First, they ensure consistency, which makes comments easier to read and understand. 
  -  Second,they help to ensure that you actually write comments. if you don't have a clear idea what you are going to comment and how, it's easy to end up writing no comments at all.

 > Most comments fall into one of the following categories:
 ### Interface
 - A comment block that immediately precedes the declaration of a module such as a class, data structure, function, or method. The comment describe's the modules's interface.
    - For a class, the comment describes the overall abstraction provided by the class.
    - For a method or function, the comment describes its overall behavior, its arguments and return value, 
    - if any any side effects or exceptions that it generates, and any other requirements the caller mush satisfy before invoking the method.
 ### Data structure member
 - a comment next to the declarations of a field in a data structure, such as an instance variable or static variable for a class.
 ### Implementation comment
 - a comment inside the code of a method or function, which describes how the code works internally
 ### Cross-module comment
 - a comment describing dependencies that cross modules boundaries

 > The most important comments are those in the first two categories. Every class should have an interface comment, every class variable should have a comment, and every method should have an interface comment. Occasionally, the declaration for a variable or method is so obvious that there is nothing useful to add in a comment(like getters and setters) but this is error; It's easier to comment everything rather than spend energy worrying about whether comment is needed.
  - Cross-module comments are the most rare of all and they are problematic to write, but when they are needed they are quite important.

## 13.2 Don't repeat the code 
 > Unfortunately, many comments are not particularly helpful. The most common reason is that the comments repeat the code: all of the information in the comment can easily be deduced from the code next to the comment.
 - if you notice that comments are roughly the same level of detail as the code. It's redundant.

 > After you have written a comment, ask yourself the following question:
 - Could someone who has never seen the code write the comment just by looking at the code next to the comment?
   - If the answer is yes, as in the examples, then the comment doesn't make the code any easier to understand.
   - Those comments are the reason why some people think that comments are worthless

 > Another common mistake is to use the same words in the comment that appear in the name of the entity being documented:
  - That is also giving any value to the reader of the comment as it's pretty much the same information as the next lines.

## Red Flag: Comment Repeats Code
 - If the information in a comment is already obvious from the code next to the comment, then the comment isn't helpful. One example of this is when the comment uses the same words that make up the name of the thing it's describing.

 > At the same time, there is important information that is missing from the comments: 
 - For example, what is a "normalized resource name", and what are the elements of the array returned by `getNormalizedResource-Names`? What does "downcast" mean?
 - What are the units of padding, and is the padding on one side of each line or both?
 - Describing these things in comments would be helpful.

 > A first step towards writing good comments is to **use different words in the comment from those in the name of the entity being described.** Pick words for the comment that provide additional information about the meaning of the entity, rather than just repeating its name.
 - Comment that provides additional information that is not obvious from the declaration itself.

 ## 13.3 Lower-level comments add precision
  > **Comments are argument the code by providing information at a different level of detail.** Some comments provide information at a lower, more detailed, level than the code; these comments add *precision* by clarifying the exact meaning of the code.
 - Other comments provide information at a higher, more abstract, level than the code; those comments offer *intuition*, such as the reasoning behind the code, or a simpler and more abstract way of thinking about the code.
 - Comments at the same level as the code are likely to repeat the code.(Which is not an ideal)

 > Precision is most useful when commenting variable declarations such as class instance variables, method arguments, and return values. The name and type in a variable declaration are typically not very precise.
 - Comments can fill in missing details such as:
   - What are the units for this variable?
   - Are the boundary conditions inclusive or exclusive?
   - In a null value is permitted, what does it imply?
   - If a variable refers to a resource that must eventually be freed or closed, who is responsible for freeing or closing it?
   - Are there certain properties that are always true for the variable(*invariants*, means never changes) such as "this list always contains at lease one entry"?

 > Some of this information could potentially be figured out by examining all of the code where the variable is used. However, this is time-consuming and error-prone; the declarations's comment should be clear and complete enough to make this unnecessary.
  - When I say that the comment for a declaration should describe things that aren't obvious from the code, "the code" refers to the code next to the comment(the declaration). not "all of the code in the application."

 > The most common problem comments for variables is that the comments are too vague. Here are two examples of comments that aren't precise enough:
 ```
 // Current offset in resp Buffer 
  uint32_t offset; 

 // Contains all line-widths inside the document and 
 // number of appearances. 
  private TreeMap<Integer, Integer> lineWidths;
 ```
 > In the first example it's not clear what "current" means. In the second example, it's not clear that the keys in the `TreeMap` are line widths and values are occurrence counts. Also, are widths measured in pixels or characters? The revised comment below provide additional details:
 ```
 //  Position in this buffer of the first object that hasn't 
 //  been returned to the client. 
 uint32_t offset;

//  Holds statistics about line lengths of the form <length, count> 
//  where length is the number of characters in a line (including //  the newline), and count is the number of lines with 
//  exactly that many characters. If there are no lines with 
//  a particular length, then there is no entry for that length. private TreeMap<Integer, Integer> numLinesWithLength;
```

 - The second declaration uses a longer name that conveys more information. It also changes "width" to "length", because this term is more likely to make people think that the units are characters rather than pixels. Notice that the second comments documents not only the details of each entry, but also what it means if an entry is missing.

 - When documenting a variable, think *nouns*, not *verbs*. In other words, focus on what the variable represents, not how it's manipulated.

## 13.4 Higher-level comments enhance intuition
 > The second way in which comments can augment code is by providing intuition. These comments are written at a higher level than the code. This approach is commonly used for comments inside methods, and for interface comments./

 > Higher level comments are more difficult to write than lower-level comments because you must think about the code in a different way.
  - Ask yourself: What is this code trying to do?
  - What is the simplest thing you can say that explains everything in the code?
  - What is the most important thing about this code?

 > Engineers then to be very detail-oriented. We love details and are good at managing lots of them; this is essential for being a good engineer. But great software designers can also step back from the details and think about a system at a higher level.
 - This means deciding which aspects of the system are most important, and being able to ignore the low-level details and think about the system only in terms of its most fundamental characteristics.
   - This is the essence of abstraction(finding a simple way to think about a complex entity), and it's also what you must do when writing higher-level comments.
  - A good higher-level comment expresses one or a few simple ideas that provide a conceptual framework, such a "append to an existing RPC." Give the framework, it becomes easy to see how specific code statements relate to the overall goal.
  - Comments of the form "how we get here" are very useful for helping people to understand code.

## 13.5. Interface documentation
 > One of the most important roles for comments is to define abstractions. An abstraction is a simplified view of an entity, which preserves essential information but omits details that can safely be ignored.
 - **If you want code that presents good abstractions, you must document those abstractions with comments.**

 > The first step in documenting abstractions is to separate *interface comments* and *implementation comments*. 
 - Interface comments provide information that someone needs to know in order to user a class or method; they define the abstraction.
 - Implementation comments describe how a class or method works internally in order to implement the abstraction.
 - It's important to separate these two kinds of comments, so that users of an interface  are not exposed to implementation detail.

 > Furthermore, these two forms had better be different. **If interface comments must also describe the implementation, then the class or method is shallow**
  - This mean that the act of writing comments can provide clues about the quality of a design
  - The interface comment for a class provides a high-level description of the abstraction provided by the class, such as the following;

```
/** 
* This class implements a simple server-side interface to the HTTP 
* protocol: by using this class, an application can receive HTTP 
* requests, process them, and return responses. Each instance of 
* this class corresponds to a particular socket used to receive 
* requests. The current implementation is single-threaded and 
* processes one request at a time. 
*/ 
public class Http {...}
```

 - This comment above describes the overall capabilities of the class, without any implementation details or even the specifics of particular methods.
 - Finally, the comments describe the limitations of the class, which may be important to developers contemplating whether to use it.

 > The interface comment for a method includes both higher-level information for abstraction and lower-level details for precision:
 - The comment usually starts with a sentence or two describing the behavior of the method as perceived by callers; this is the higher-level abstraction.
 - The comment must describe each argument and the return value(if any). These comments must be very precise, and must describe any constraints on argument values as well as dependencies between arguments.
 - If the method has any side effects, these must be documented in the interface comment. A side effect is any consequence of the method that affects the future behavior of the system but is not part of the result. For example, if the method adds a value to an internal data structure, which can be retrieved by future method calls, this is a side effect; writing to the file system is also a side effect.
 - A method's interface comment must describe any exceptions that can emanate the method
 - If there are any preconditions that must be satisfied before a method is invoked, these must be described (perhaps some other method must be invoked first; for a binary search method, the list being searched must be sorted). It is a good idea to minimize preconditions, but any that remain must be documented.
 - The developer shouldn't need to read the body of the method in order to invoke it, and the interface comment provides no information about how the method is implemented, such as how it scans its internal data structures to find the desired data.

 ## RED FLAG: Implementation Documentation Contaminates Interface
  - This red flag occurs when interface documentation, such as that for a method, describes implementation details that aren't needed in order to use the think being documented.

 ## 13.6 Implementation comments: what and why, not how
 > Implementation comments are the comments that appear inside methods to help readers understand how they work internally. Most methods are so short and simple that they don't need any implementation comments: given the code and the interface comments, it's easy to figure out how a method works.
  - **The main goad of implementation comments is to help readers understand what the code is doing(not how it does).**
  - Once the readers know what the code is trying to do, it's usually easy to understand how the code works.

 > In addition to describing *what* the code is doing, implementation comments are also useful to explain *why*. If there are tricky aspects to the code that won't be obvious from reading it, you should document them.
  - Add a small comment if some additional lines when you're working on a bug fix.

 > For longer methods, it can be helpful to write comments for a few of the most important local variables. However, most local variables don't need documentation if they have good names.
  - If all of the uses of a variable are visible within a few lines of each other, it's usually easy to understand the variables's purpose without a comment.
    - In this case it's OK to let readers read the code to figure out the meaning of the variable.
    - However, if the variable is used over a large span of code, then you should consider adding a comment to describe the variable.
  - When documenting variables, focus on *what* the variable represents, not how it is manipulated in the code.

 ## 13.7 Cross-module design decisions
 > In a perfect world, every important design decision would be encapsulated within a single class. Unfortunately, real systems inevitably end up with design decisions that affect multiple classes. Cross-module decision are often complex and subtle, and they account for many bugs, so good documentation for them is crucial.
 - The biggest challenge with cross-module documentation is finding a place to put it where it will naturally be discovered by developers.

 > Unfortunately, in many cases there's not an obvious central place to put cross-module documentation. So where the comment should be placed(in my opinion it should be placed at the beginning of the flow)
  - One solution could be at the place where the flow begins.
  - Second solution is to write detailed comment and leave point the comment in other places.
    - With this approach, there's only a single copy of the documentation and it's relatively easy for developers to find it when they need it.
    - However, this has the disadvantage that the documentation is not near any of the pieces of code that depend on it, so it may be difficult to keep up-to-date as the system evolves.(This is the same problem as wiki like documents)

 ## Conclusion
 - The goal of comments is to ensure that the structure and behavior of the system is obvious to readers, so they can quickly find the information they need and make modifications to the system with confidence that they will work.
 - There's a significant amount of information that can't easily be deduced from the code. Comments fill in this information.
 - When writing comments, try to put yourself in the mindset of the reader and ask yourself what are the key things he or she will need to know.
 - If your code is undergoing review and a reviewer tells you that something is not obvious, **DON'T** argue with them; if a reader thinks it's not obvious, then it's not obvious. Instead of arguing, try to understand what they found confusion and see if you can clarify that, either with better comments or better code.