# Chapter 14

## Choosing Name
 > Selecting names for variables, methods, and other entities is one of the most underrated aspects of software design. Good names are form of documentation: they make code easier to understand. They reduce the need for other documentation and make it easier to detect errors.
 - Conversely, poor name choices increase the complexity of code and create ambiguities and misunderstandings that can result in bugs.

## 14.1 Example: bad names cause bugs
 > Sometimes even a single poorly names variable can have severe consequences. Unfortunately, most developers don't spend much time thinking about names. They tend to use the first name that comes to mind, as long as it's reasonably close to matching the thing it names.
 - You shouldn't settle for names that are just "reasonably close".
   - Take a bit of extra time  to choose great names, which are precise, unambiguous, and intuitive. The extra attention will pay for itself quickly, and over time you'll learn to choose good names quickly.

 ## 14.2 Create an image
  > When choosing a name, the goal is to create an image in the mind of the reader about the nature of the thing being named. A good name conveys a lot of information about what the underlying entity is, and, just as important, what it is not. 
  - When considering a particular name, ask yourself: "*If someone sees his name in isolation, without seeing its declaration, its documentation, or any code that uses the name, how closely will they be able to guess what the name refers to? Is there some other name that will paint a clearer picture?*"
    - Of course, there's a limit to how much information you can put in a single name; names become unwieldy if they contain more than two or three words. Thus, the challenge is to find just a few words that capture the most important aspects of the entity

 > Names are a form of abstraction: they provide a simplified way of thinking about a more complex underlying entity. 
 - Like other forms of abstraction, the best names are those that focus attention on what is most important about the underlying entity while omitting details that are less important.

## 14.3 Names should be precise
 > Good names have two properties: precision and consistency. The most common problem with names is that they are too generic or vague; as a result, it's hard for readers to tell what the name refers to; the reader may assume that the name refers to something different from reality.

## RED FLAG: Vague Name
 - If a variable or method name is broad enough to refer to many different things, then it doesn't convey much information to the developer and the underlying entity is more likely to be misused.

 > Like all rules, the rule about choosing precise names has a few exceptions. For example, it's fine to use generic names like *i* and *j* as loop iteration variables, as long as the loops only span a few lines of code. 
  - If you can see the entire range of usage of a variable, then the meaning of the variable will probably be obvious from the code so you don't need a long name.
```
for  (i = 0; i < numLines; i++) { ... }
```
 - It's clear from this code that *i* is being used to iterate over each of the lines in some entity. If the loop gets so long that you can't see it all at once, or if the meaning of the iteration variable is harder to figure out from the code, then a more descriptive name is in order.

 > It's also possible for a name to be too specific, such as in this declaration for a method that deletes a range of text:
 ```
 void delete(Range selection) {...}
 ```
 - The argument name *selection* is too specific, since it suggests that the text being deleted is always selected in the user interface. However, this method can be invoked on any range of text, selected or not. Thus, the argument name should be more generic such as *range*.

 > If you find it difficult to come up with a name for a particular variable that is precise, intuitive, and not too long, this is a red flag. It suggests that the variable may not have a clear definition or purpose. When this happens, consider alternative factorings. 
 - For example, perhaps you are trying to use a single variable to represent several things; if so, separating the representation into multiple variables may result in a simpler definition for each variable. 
 - The process of choosing good names can improve your design by identifying weaknesses.

## RED FLAG: Hard to Pick Name
 - If it's hard to find a simple name for a variable or method that creates a clear image of the underlying object, that's a hint that the underlying object may not have a clean design.

## Use names consistency
 > The second important property of good names is consistency. In any program there are certain variables that are used over and over again. For example, a file system manipulates block numbers repeatedly. For each of these common usages, pick a name to use for that purpose, and use the same name everywhere.
 - Consistent naming reduces cognitive load in much the same way as reusing a common class: once the reader has seen the name in one context, they can reuse their knowledge and instantly make assumptions when they see the name in a different context.

 > Consistency has three requirements
 1. first, always use the common name for the given purpose
 2. second, never use the common name for anything other than the given purpose
 3. third, make sure that the purpose is narrow enough that all variables with the name have the same behavior.

 > Sometimes you will need multiple variables that refer to the same general sort of thing. For example, a method that copies file data will need two block numbers, one for the source and one for the destination. When this happens, use the common name for each variable but add a distinguishing prefix, such a *srcFileBlock* and *dstFileBlock*.
  - Loops are another area where consistent naming can help. If you use names such a *i* and *j* for loop variables, always use *i* in outermost loops and *j* for nested loops.
    - This allows readers to make instant(safe) assumptions about what's happening in the code when they see a given name.

## 14.5 A different opinion: Go style guide
> Overall, I would argue that readability must be determined by readers, not writers. If you write code with short variable names and the people who read it find it easy to understand, then that's fine. If you start getting complains that your code is cryptic, then you should consider using longer names(a Web search for "go language sort names" will identify several such complaints). Similarly, if I start getting complaints that long variable names make my code harder to read, then I'll consider using shorter ones.

## 14.6 Conclusion
 > Well chosen help to make code more obvious; when someone encounters the variable for the first time, their first guess about behavior, made without much thought, will be correct. 
 - If you take a little extra time up front select good names, it will be easier for you to work on the code in the future.
 - In addition, you will be less likely to to introduce bugs. Developing a skill for naming is also an investment.
 - When you first decide to stop settling for mediocre names, you may find it frustrating and time-consuming to come up with good names. However, as you get more experience you'll find that it becomes easier; eventually, you'll get to the point where it takes almost no extra time to choose good names, so you'll get the benefits almost for free.