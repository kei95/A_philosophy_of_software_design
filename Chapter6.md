# Chapter 6

## General-Purpose Modules are Deeper
 > One of the most common decisions that you will face when designing a new module is whether to implement it in a general-purpose or special-purpose fashion.\
 > we know that it’s hard to predict the future needs of a software system, so a general-purpose solution might include facilities that are never actually needed.

  ## 6.1 Make classes somewhat general-purpose
  > In my experience, the sweet spot is to implement new modules in a somewhat general-purpose fashion. The phrase “*somewhat general-purpose*” means that the module’s functionality should reflect your current needs, but its interface should not.\
 > Instead, the interface should be general enough to support multiple uses.
 - The interface should be easy to use for today’s needs without being tied specifically to them.
 - The word “somewhat” is important: don’t get carried away and build something so general-purpose that it is difficult to use for your current needs.

 > The most important (and perhaps surprising) benefit of the general-purpose approach is that it results in simpler and deeper interfaces than a special-purpose approach.
 - The general-purpose approach can also save you time in the future, if you reuse the class for other purposes.
   - However, even if the module is only used for its original purpose, the general-purpose approach is still better because of its simplicity.
 - ***Making specific modules tends to create shallow modules as a result***

 ## 6.4 A Generally leads to better information hiding
  > The general-purpose approach provides a cleaner separation between the text and user interface classes, which results in better information hiding.
 - One of the most important elements of software design is determining who needs to know what, and when.
 - When the details are important, it is better to make them explicit and as obvious as possible, such as the revised implementation of the backspace operation.
   - Hiding this information behind an interface just creates obscurity.

## 6.5 Questions to ask yourself
 > It is easier to recognize a clean general-purpose class design than it is to create one. Here are some questions you can ask yourself, which will help you to find the right balance between general-purpose and special-purpose for an interface.

 ### **What is the simplest interface that will cover all my current needs?**
  - If you reduce the number of methods in an API without reducing its overall capabilities, then you are probably creating more general-purpose methods.
 - Reducing the number of methods makes sense only as long as the API for each individual method stays simple;
   - ***if you have to introduce lots of additional arguments in order to reduce the number of methods, then you may not really be simplifying things.***

### **In how many situations will this method be used?**
 - If a method is designed for one particular use, such as the *backspace method*, that is a red flag that it may be too special-purpose.
 - See if you can replace several special-purpose methods with a single general-purpose method.

### **Is this API easy to use for my current needs?**
 - This question can help you to determine when you have gone too far in making an API simple and general-purpose.
 - If you have to write a lot of additional code to use a class for your current purpose, that’s a red flag that the interface doesn’t provide the right functionality.

## 6.6 Conclusion
 - General-purpose interfaces have many advantages over special-purpose ones.
 - They tend to be simpler, with fewer methods that are deeper.
 - They also provide a cleaner separation between classes, whereas special-purpose interfaces tend to leak information between classes.
 - ***Making your modules somewhat general-purpose is one of the best ways to reduce overall system complexity.***