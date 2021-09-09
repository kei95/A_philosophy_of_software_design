# Chapter 2

## The Nature of Complexity

### What is complexity?
 >  Complexity is anything related to the structure of a software system that makes it hard to understand and modify the system.\
 > ...If a software system is hard to understand and modify, then it is complicated; if it's easy to understand and modify, then it's simple
 - It's important to follow my intuition to judge if the software is complicated or not.

 > Complexity is what a developer experiences at a particular point in time when trying to achieve a particular goal. It doesn't necessarily relate to the overall size or functionality of the system.
  - So scale of the system doesn't matter to decide wether if it's "complex" or not.

 > Complexity is determined by the activities that are most common. If a system has a few parts that are very complicated, but not need to be touched, then they don't have much impact on the overall complexity of the system.\
> Isolating complexity in a place where it will never be seen is almost good as eliminating the complexity entirely.
 - The place of the project matters to weigh the complexity. If I could successfully isolate complex place, that means it's a success in this books principle

> Complexity is more apparent to readers than writers. If you write a piece of code and it seems simple to you, but other people think it is complex, then it is complex.\
> Your job as a developer is not just to create code that you can work with easily, but to create code that others can work with easily

## 2.2 Symptoms of complexity
###  Change amplification
 > The first symptom of complexity is that seemingly simple change requires code modification in many different places
 - I actually feel it right now. If you are spending much more time to fix single UI bug absolutely indicates the architecture is complex.
 - If changing single/several lines fixes the bug/change, it is a good architecture

### Cognitive load
 > The second symptom of complexity is cognitive load, which refers to how much a developer needs to know in order to complete a task.\
 >A higher cognitive load means that developers have to spend more time learning the required information.
  - **Sometimes an approach that requires more lines of code is actually simpler, because if reduces cognitive load**

### Unknown unknowns
 > The third symptom of complexity is that it's not obvious which pieces of code must be modified to complete a task, or what information a developer must have to carry out the task successfully.
 - Each parts of functionalities of code should self explanatory in order to accomplish the change easily.

> Of the three manifestations of complexity, unknown unknown are the worst. An unknown unknown means that there is something you need to know, but there's no way for you to find out what it is, or even whether there's is an issue. You won't find out about is until bugs appear after you make a change.
 - One of the most important goal of good design is for a system to be *Obvious*

## 2.3 Causes of complexity
  > Complexity is caused by two things: *dependencies* and *obscurity*

### Dependency
 - A dependency exists when a given piece of code cannot be understood and modified in isolation.
 - Dependencies are fundamental part of software and can't be completely eliminated.

### Obscurity
 - Obscurity occurs when important information is not obvious.
 - A simple expample is a variable name that is so generic that it doesn't carry much useful information(like time).
    - inconsistency iis also a major contributor to obscurity, if the same variable name is used fro two different purposes, it won't be obvious to developer which of these purposes a particular variable serves.
 - The best way to reduce obscurity is by simplifying the system design

> Dependencies lead to change amplification and a high cognitive load. Obscurity creates unknown unknowns, and also contributes to cognitive load.
 - If we can find design techniques that minimize dependencies and obscurity, then we can reduce the complexity of software.

## 2.4 Complexity is incremental
 > Complexity isn't caused by a single catastrophic error; it accumulates in lots of small chunks.\
 > Complexity comes about because hundreds or thousands of small dependencies and obscurities build up over time.
 - Working on something piled up for years is not a easy job, but it's a good chance to see bad examples at the same time.

> It's easy to convince yourself that a little bit of complexity introduced by your current change is no big deal. However, if every developer takes this approach for every change, complexity accumulates rapidly.
 - It's important to eliminate complexity for even small changes. If the complexity accumulates, it's hard to eliminate.
 - **ZERO TOLERANCE** for complexity is the key.

## 2.5 Conclusion
> Complexity comes from an accumulation of dependencies and obscurities. As complexity increases, it leads to change amplification, a high cognitive load, and unknown unknowns. As a result, it takes more code modifications to implement each new feature. In addition, developers spend more time acquiring enough information to make the change safely and, in the worst case, they can’t even find all the information they need. The bottom line is that complexity makes it difficult and risky to modify an existing code base.
