# Chapter 16

## Modifying Existing code
 > Chapter 1 described how software development is iterative and incremental. A large software system develops through a series of evolutionary stages, where each stage adds new capabilities and modifies existing modules.

## 16.1 Stay strategic
 > In tactical programming, the primary goal is to get something working quickly, even if that results in additional complexity; in strategic programming, the most important goal is to produce a great system design.
 - If you want to have a system that is easy to main maintain and enhance, then "working" isn't a high enough standard; you have to prioritize design and think strategically.
   - The idea also applies when you are modifying existing code.

 > Unfortunately, when developers go into existing code to make changes such as bug fixes or new features, they don't usually think strategically. A typical mindset is "what is the smallest possible change I can make that does what I need?" Sometimes developers justify this because they are not comfortable with the code being modified; they worry that larger changes carry a greater risk of introducing new bugs.
  - However, this results in tactical programming. Each one of these minimal changes introduces a few special cases, dependencies, or other forms of complexity.
  - As a result, the system design gets just a bit worse, and the problems accumulate with each step in the system's evolution.

 > If you want to maintain a clean design for a system, you must take a strategic approach when modifying existing code.
 - **Ideally, when you have finished with each change, the system will have the structure it would have had if you had designed it from the start with that change in mind.**
 - If the system is not the best way to implement, refactor the system so that you end up with the best possible design.
   - With this approach, the system design improves with every modification.

 > If you invest a little extra time to refactor and improve the system design, you'll end up with a cleaner system. This will speed up development, and you will recoup the effort that you invested in the refactoring.
 - You should still be on the lookout for design imperfections that you can fix while you're in the code.
 - **If you're not making the design better, you are probably making it worse.**

 ## 16.2 Maintaining comments: keep the comments near the code
 > When you change existing code, there's a good chance that the changes will invalidate some of existing comments. It's easy to forget to update comments when you modify code, which results in comments that are no longer accurate. 
 - Inaccurate comments are frustrating to readers, and if there are very many of them, readers begin to distrust all of the comments.
 - Fortunately, with a little discipline and a couple of guiding rules, it's possible to keep comments up-to-date without a huge effort.

 > **The best way to ensure that comments get updated is to position them close to the code they describe,** so developers will see them when they change the code.
  - The farther a comment is from its associated code, the less likely it is that it will be updated properly.

 > When writing implementation comments, don't put all the comments for an entire method at the top of the method. Spread them out, pushing each comment down to th narrowest scope that includes all of the code referred to by the comment.
 - For example, if a method has three major phases, don't write one comment at the top of the method that describes all of the phases in detail. Instead, write a separate comment for each phase and position that comment just above the first line of code in that phase.
 - On the other hand, it can also be helpful to have a comment at the top of a method's implementation that describes the overall strategy, like this:
```
//  We proceed in three phases: 
//  Phase 1: Find feasible candidates 
//  Phase 2: Assign each candidate a score 
//  Phase 3: Choose the best, and remove it
```
 - **In general, the farther a comment is from the code it describes, the more abstract it should be**(this reduces the likelihood that the comment will be invalidated by code changes)

 ## Comments belong in the code, not the commit log
 > A common mistake when modifying code is to put detailed information about the change in the commit message for the source code repository, but then not to document it in the code.
 - Although commit messages can be browsed in the future by scanning the repository's log, a developer who needs the information is unlikely to think of scanning the repository log. Even if they do scan the log, it will be tedious to find the right log message.

 > When writing a commit message, ask yourself whether developers will need to use that information in the future. If so, then document this information in the code. An example is a commit message describing a subtle problem that motivated a code change. If this isn't documented in the code, then a developer might come along later and undo the change without realizing that they have re-created a bug.
 - This illustrates the principle of placing documentation in the place where developers are most likely to see it; the commit log is rarely that place.

 ## 16.4 Maintaining comments: avoid duplication
  > The second technique for keeping comments up to date is to avoid duplication. If documentation is duplicated, it is more difficult for developers to find and update all of the relevant copies. Instead, try to document each design decision exactly once.
 - If there are multiple places in the code that are affected by a particular decision, don't repeat the documentation at each of these points.  Instead, find the most obvious single place to put the documentation.

 > If there's no "obvious" single place to put a particular piece of documentation where developers will find it, create a designNotes file. Or, pick the best of the available places and put the documentation there. In addition, add short comments in the other places that refer to the central location: "See the comment in XYZ for an explanation of the code below:"
  - If the reference becomes obsolete because the master comment was moved or deleted, this inconsistency will be self-evident because developers won't find the comment at the indicated place; they can use revision control history to find out what happened to the comment and then update the reference.
    - In contrast, if the documentation is duplicated and some of the copies don't get updated, there will be no indication to developers that they are using stale information.

 > Don't redocument one module's design decisions in another module. For example, don't put comments before a method call that explain what happens in the called method. If readers want to know, they should look at the interface comments for the method.
 - **If information is already documented someplace outside your program, don't repeat the documentation inside the program; just reference the external documentation.**
 - It's important that readers can easily find all the documentation need to understand your code, but that doesn't mean you have to write all of that documentation.

 ## 16.5 Maintaining comments: check the diffs
  > One good way to make sure documentation stays up to date is to take a few minutes before committing a change to your revision control system to scan over all the changes for that commit; make sure that each change is properly reflected in the documentation.
  - These pre-commit scans will also detect several other problems, such as accidentally leaving debugging code in the system or failing to fix TODO items.

 ## 16.6 Higher-level comments are easier to maintain
  > One final thought on maintaining documentation: comments are easier to maintain if they are higher-level and more abstract than the code. These comments do not reflect the details of the code, so they will not be affected by minor code changes; only changes in overall behavior will affect these comments.
  - of course, some comments do need to be detailed and precise. But in general, the comments that are most useful(they don't simply repeat the code) are also easiest to maintain.