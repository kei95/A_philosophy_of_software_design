# Chapter 21

## Conclusion
  > The book is about one thing: **Complexity**.
   - Dealing with complexity is the most important challenge in software design. It's what makes systems hard to build and maintain, and it often makes them slow as well.

 > Over the course of the book I have tried to describe the root causes that lead to complexity, such as dependencies and obscurity. I have discussed red flags that can help you identify unnecessary complexity, such as information leakage, unneeded error conditions, or names that are too generic. I have presented some general ideas you can use to create simpler software systems, such as striving for classes that are deep and generic, defining errors out of existence, and separating interface documentation from implementation documentation. And, finally, I have discussed the investment mindset needed to produce simple designs.
 - The downside of all these suggestions is that they will create extra work in the early stages of a project.
   - It even takes longer if you are not used to thinking about design issues while you lean good design techniques.
   - If the only thing that matters to you is making your current code work asap, then thinking about design will seem like drudge work that is getting in the way of your goal.
   - On the other hand, if good design is an important goal for you, then the ideals in this book should make programming more fun. Design is a fascinating puzzle. It's fun to explore different approaches, and it's a great feeling ot discover a solution that is both simple and powerful. A clean, simple, and obvious design is a beautiful thing.

 > Furthermore, the investments you make in good design will pay off quickly.
 - The modules you defined carefully at the beginning of a project will save you time later as you reuse them over and over.
 - The clear documentation that you wrote six months ago will save you time when you return to the code to add a new feature.
 - The time you spent honing your design skills will also pay for itself: as your skills and experience grow, you will find that you can produce good designs more and more quickly. Good design doesn't really take much longer than quick-and-dirty design, once you know how.

- The reward for being a good designer is that you get to spend a larger fraction of your time in the design phase, which is fun. Poor designers spend most of their time chasing bugs in complicated and brittle code. If you improve your design skills, not only will you produce higher quality software more quickly, but the software development process will be more enjoyable.

## Summary of Design Principles
1. Complexity is incremental: you have to sweat the small stuff (see p. 11). 
2. Working code isn’t enough (see p. 14). 
3. Make continual small investments to improve system design (see p. 15). 
4. Modules should be deep (see p. 22)
5. Interfaces should be designed to make the most common usage as simple as possible (see p. 27). 
6. It’s more important for a module to have a simple interface than a simple implementation (see pp. 55, 71). 
7. General-purpose modules are deeper (see p. 39). 
8. Separate general-purpose and special-purpose code (see p. 62). 
9. Different layers should have different abstractions (see p. 45). 
10. Pull complexity downward (see p. 55). 
11. Define errors (and special cases) out of existence (see p. 79). 
12. Design it twice (see p. 91). 
13. Comments should describe things that are not obvious from the code (see p. 101). 
14. Software should be designed for ease of reading, not ease of writing (see p. 149). 
15. The increments of software development should be abstractions, not features

