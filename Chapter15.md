# Chapter 15

## Write The Comments First(Use Comments As Part Of The Design Process)
 > Many developers put off writing documentation until the end of the development process, after coding and unit testing are complete. 
 - This is one of the surest ways to produce poor quality documentation.
 - The best time to write comments is at the *beginning* of the process, as you write the code.
 - Writing the comments first makes documentation part of the design process.

## 15.1 Delayed comments are bad comments
 > Almost every developer I have every met puts off writing comments. When asked why they don't write documentation earlier, they say that the code is still changing. If they write documentation early, they say, they'll have to rewrite it when the code changes; better to wait until the code stabilizes. However, I suspect that there's another reason, which is that they view documentation as drudge work; thus, they put if off as long as possible.
  - Unfortunately, this approach has several negative consequences.
    - First, delaying documentation often means that if never gets written at all. Once you start delaying, it's easy to delay a bit more; after all, the code will be even more stable in a few more weeks.
      - By the time the code has unarguably stabilized, there is a lot of it, which means the task of writing documentation has become huge and even less attractive.
      - There's never a convenient time to stop for a few days and fill in all of the missing comments, and it's easy to rationalize that the best thing for the project is to move on and fix bugs or write the next new feature. This will create even more undocumented code.

 > Even if you do have the self-discipline to go back and write the comments(and don't fool yourself: you probably don't), the comments won't be very good. By this time in the process, you have checked out mentally. You just want to get through it as quickly as possible. Thus, you make a quick pass over the code, adding just enough comments to look respectable.
 - At the end, when you look at the code as you are writing the comments, so the comments repeat the code.
 - So you'll end up missing some of the most important things they should be describe.

 ## Write the comments first
  > I use a different approach to writing comments, where I write the comments at the very beginning:
 - For a new class, I start by writing the class interface comment.
 - Next, I write interface comments and signatures for the most important public methods, but I leave the method bodies empty.
 - I iterate a bit over these comments until the basic structure feels about right.
 - At this point I write declarations and comments for the most important class instance variables in the class.
 - Finally, I fill in the bodies of the methods, adding implementation comments as needed.
 - While writing method bodies, I usually discover the need for additional methods and instance variables. For each new method I write the interface comment before the body of the method; for instance variables I fill in the comment at the same time that I write the variable declaration.
 - So overall, when the code is done, the comments are also done. There's never a backlog of unwritten comments.

 ## Comments are design tool
  > The second, and most important, benefit of writing the comments at the beginning is that it improves the system design. Comments provide the only way to fully capture abstractions, and good abstractions are fundamental to good system design. If you write comments describing the abstractions at the beginning, you can review and tune them before writing implementation code.
  - To write a good comment, you must identify the essence of a variable or piece of code: What are the most important aspects of this thing?
    - It's important to do this early in the design process; otherwise ***you are just hacking code***.

 > Comments serve as a canary in the coal mine of complexity. If a method or variable requires a long comments, it's a red flag that you don't have a good abstraction. Remember classes should be deep: the best classes have very simple interfaces yet implement powerful functions.
 - The best way to judge the complexity of an interface is from the comments that describe it.
   - If the interface comment for a method provides all the information needed to use the method and is also short and simple, that indicates that the method has a simple interface.
 - Conversely, if there’s no way to describe a method completely without a long and complicated comment, then the method has a complex interface.
 - If the interface comment must describe all the major features of the implementation, then the method is **shallow**
 - The same idea applies to variables
   - If it takes a long comment to fully describe a variable, it's a red flag that suggests you may not have chosen the right variable decomposition.

## RED FLAG: Hard to Describe
 - The comment that describes a method or variable should be simple and yet complete. If you find it difficult to write such a comment, that's an indicator that there may be a problem with the design of the thing you are describing.

 > Of course, comments are only a good indicator of complexity if they are complete and clear. If you write a method interface comment that doesn't provide all the information needed to invoke the method, or one that is so cryptic that it's hard to understand, then that comment doesn't provide a good measure of the method's depth.

 ## 15.4 Early comments are fun comments
  > The third and final benefit of writing comments early is that is makes comment-writing more fun. For me, one of the most enjoyable parts of programming is the early design phase for a new class, where I'm fleshing out the abstractions and structure for the class.
 - The simpler the comments, the better I feel about my design, so finding simple comments is a source of pride.
 - If you are programming strategically, where your main goal is a great design rather than just writing code that works, then writing comments should be fun, since that's how you identify the best designs.

 ## 15.6 Conclusion
 - If you haven't tried writing the comments first, give it a try. Stick with it long enough to get used to it. Then think about how it affects the quality of your comments, the quality of your design, and  your overall enjoyment of software development.