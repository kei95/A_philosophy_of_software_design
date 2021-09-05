# Chapter 1

## Introduction(It’s all about complexity)

> All programming requires is a creative mind and the ability to organize your thoughts. … This means that the greatest limitation in writing software is our ability to understand the systems we are creating.\
> The larger the program, and the more people that work on it, the more difficult it is to manage complexity.
-  As software gets bigger(industry/technology wise), the complexity increases inevitably that causes difficulty in understanding or keep all of the relevant factors in their minds as they modify the system.
  - As Justin mentioned earlier, it’s not important to use complex tools/frameworks to implement something in a development(it’s you, redux-saga).

<br/>

> There’re two general approaches to fighting complexity.
> The first is to eliminate complexity by making code simpler and more obvious.
- e.g. eliminating special cases, using identifiers in a consistent fashion etc.

<br/>

> The second is to encapsulate it, so that programmers can work on a system without being exposed to all of its complexity at once.
- This approach is called ***modular design***
  - In this design, software system is divided up into modules, such as classes in an object-oriented language.
  - The modules are designed to be relatively independent of each other.
  - The goal is to make it possible for other developers to work on one module without having to understand the details of other modules.

<br/>

> The waterfall model is not structured to accommodate major design changes after the initialization. Thus developers try to patch around the problems without changing the overall design. This results in an explosion of complexity.
- The reason why waterfall is not a thing these days.

<br/>

> Software development projects today use an incremental approach such as ***agile development*** in which the initial design focuses on a small subset of the overall functionality. The subset is designed, implemented, and then evaluated. Problems with the original design are discovered and corrected, then few more features are designed, implemented and evaluated.
- However, I saw teams that forces designer to create whole design of the feature before even implementation begins and the designer keeps move on to next one. The team ended up in patch around the small problems as they go since the designer is too busy working on next.
  - This is super bad as it creates complexity drastically(only someone knows what’s going on kind of problem) and is exactly the same as the cons that mentioned in waterfall.

<br/>

> As a software developer, you should always be on the lookout for opportunities to improve the design of the system you are working on, and you should plan on spending some fraction of your time on design improvements.
> If software developers should always be thinking about design issues, and reducing complexity is the most important element of software design.
- It’s applicable to myself, and the team too. Just a single person changes his/her mind to care about design of the system can’t change the entire system.
  
<br/>

> This book has two overall goals. the first is to describe the nature of software complexity
> The second, is to present techniques you can use durning the software development process to minimize complexity.

<br/>

## 1.1 How to use this book
> The best way to use this book is in conjunction with code reviews. When you read other people’s code, think about whether it conforms to the concepts discussed here and how that relates to the complexity of the code.
> It’s easier to see design problems in someone else’s code than your own.
- Do not underestimate code review. ***One good turn deserves another***.

<br/>

> One of the best ways to improve your design skills is to learn to recognize red flags
- Signs that a piece of code is probably more complicated than it needs to be.

<br/>

> It’s important to use moderation and discretion. Beautiful designs reflect a balance between competing ideas and approaches.
