# Chapter 12

## Why Write Comments? The Four Excuses
 > In-code documentation plays a crucial role in software design. Comments are essential to help developers to understand a system and work efficiently, but the role of comments goes beyond this. Documentation also plays an important role in abstraction;
 - without comments, you can't hide complexity. Finally, **The process of writing comments, if done correctly, will actually improve a system's design**
 - Conversely, a good software design loses much of its value if it's poorly documented.

 > Unfortunately, this view is not universally shared. A significant fraction of production code contains essentially no comments. Many developers think that comments are a waste of time; others see the value in comments, but somehow never get around to writing them. <- It's me
  - Fortunately, many development teams recognize the value of documentation, and it feels like the prevalence of these teams is gradually increasing.
  - However, even in teams that encourage documentation, comments are often viewed as drudge work and many developers don't understand how to write them, so the resulting documentation is often mediocre.
  - Inadequate documentation creates a huge and unnecessary drag on software development.

 > In this chapter I will discuss the excuses developers use to avoid writing comments, and the reason why comments really do matter. **Chapter 13** will then describe how to write good comments and the next few chapters after that will discuss related issues such as choosing variable names and how to use documentation to improve a system's design.\
 > I hope these chapters will convince you of three things: 
 1. good comments can make a big difference in the overall quality of software
 2. it isn't hard to write good comments
 3. and(this may be hard to believe) writing comments can actually be fun.

 > When developers don't write comments, they usually justify their behavior with one or more of the following excuses:
 - "Good code is self-documenting"
 - "I don't have time to write comments"
 - "Comments get out of date and become misleading"
 - "The comments I have seen are all worthless; why bother?"

## Good code is self-documenting
 > Some people believe that if code is written well, it is so obvious that no comments are needed. This is a delicious myth, like a rumor that ice cream is good for your health: we'd really like to believe it! Unfortunately, it's simply not true. To be sure, there are things you can do when writing code to reduce the need for comments, such as choosing good variable names.
 - Nonetheless, there is still a significant amount of design information that can't be represented in code.
 - Only a small part of a class's interface, such as the signatures of its methods can be specified formally in the code.
 - The informal aspects of an interface, such as a high-level description of what each method does or the meaning of its result, can only be described in comments.

 > Some developers argue that if others want to know what a methods does, they should just read the code of the method: this will be more accurate than any comment.
  - It's possible that a reader could deduce the abstract interface of the method by reading its code, but it would be time-consuming and painful.
 - In additions if you write code with the expectation that users will read method implementations, you will try to make each method as short as possible, so that it's easy to read.
 - This will result in a large number of shallow methods. So it doesn't really make the code easier to read as they gets spread all over the place.

 > Moreover, comments are fundamental ot abstractions. the goal of abstractions is to hide complexity: an abstraction is a simplified view of an entity, which preserves essential information but omits details that can safely be ignored.
  - **If users must read  the code of a method in order to use it, then there's no abstraction:**
    - all of the complexity of the method is exposed.
  - Without comments, the only abstraction of a method is its declaration, which specifies its name and the names and types of its arguments and results.
    - The declaration is missing too much essential information to provide a useful abstraction by itself.
    - It's also important that comments are written in a human language such as English; this makes them less precise than code, but it provides more expressive power, so we can create simple, intuitive descriptions.
      - If you wan to use abstractions to hide complexity, comments are essential

 ## 12.2 I don't have time to write comments
  > It's tempting to prioritize comments lower than other development tasks. Given a choice between adding a new feature and documenting an existing feature, it seems logical to choose the new feature. However, software projects are almost always under time pressure, and there will always be things that seem higher priority than writing comments.
 - Thus, if you allow documentation to be de-prioritized, you'll end up with no documentation.

 > If you want a clean software structure, which will allow you to work efficiently over the long-term, then you must take some extra time up front in order to create that structure.
  - Good comments make a huge difference in the maintainability of software, so the effort spent on them will pay for itself quickly.
  - Writing comments needn't take a lot of time.
  - Furthermore, many of the most important comments are those related to abstractions, such as the top-level documentation for classes and methods.
immediately.

## 12.3 Comments get out of date and become misleading
 > Comments do sometimes get out of date, but this need not be a major problem in practice. Keeping documentation up-to-date doesn't require an enormous effort. Large changes to the documentation are only required if there have been large changes to the code, and the code changes will take more time than the documentation changes.
  - Code reviews provide a great mechanism for detecting and fixing stale comments.

## 12.4 All the comments I have seen are worthless
 > Of the four excuses, this is probably the one with the most merit. Every software developer has seen comments that provide no useful information, and most existing documentation is so-so at best.
  - Fortunately, this problem is solvable; writing solid documentation is not hard, once you know how.

## 12.5 Benefits of well-written comments
 > **The overall idea behind comments is to capture information that was in the mind of the designer but couldn't be represented in the code.** This information ranges from low-level details, such a hardware quirk that motivates a particularly tricky piece of code, up to high-level concepts such as the rationale for a class.
 - When other developers come along later to make modifications, the comments will allow them to work more quickly and accurately.
 - Without documentation, future developers will have to rederive(filter) or guess at the developer's original knowledge;
   - This will take additional time, and there's a risk of bugs if the new developer misunderstands the original designer's intentions.
 - Comments are valuable even when the original designer is the one making the changes: if it has been more than a few weeks since you last worked in a piece of code, you'll have forgotten many of the details of the original design.

 > Good documentation helps with **Cognitive load** and **Unknown unknowns**. 
 - Documentation can reduce cognitive lead by providing developers with the information they need to make changes and by making it easy for developers to ignore information that is irrelevant.
 - It also can reduce the unknown unknowns by clarifying the structure of the system, so that it's clear what information and code is relevant for any given change.