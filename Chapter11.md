# Chapter 11

## Design it Twice
 > Designing software is hard, so it's unlikely that your first thoughts about how to structure a module or system will produce the best design.  
 - You'll end up with a much better result if you consider multiple options for each major design decision: ***design it twice.***

 > Suppose you are designing the class that will manage the text of a file for a GUI text editor.
 - The first step is to define the interface that the class will present to the rest of the editor; rather than picking the first idea that comes to mind, consider several possibilities.
   - One choice is a line-oriented interface, with operations to insert modify, and delete whole lines of text.
   - Another option is an interface based on individual character insertions and deletions.
   - A third choice is a string-oriented interface, which operates on arbitrary ranges of characters that may cross line boundaries.
 - You don't need to pin down every feature of each alternative; it's sufficient at this point ot sketch out a few of the most important methods.

 > Try to pick approaches that are radically different from each other; you'll learn more that way. Even if you are certain that there; only one reasonable approach, consider a second design anyway, no matter how bad you think it'll be.
 - After you have roughed out the designed for the alternatives, make a list of the pros and cons of each one.
 - The most important consideration for an interface is each of use for higher level software.

 > In the example above, both the line-oriented interface and the character-oriented interface will require extra work in software that uses the text class.
 - It is also worth considering other factors:
   - Does one alternative have a simpler interface than another? In the text example, all of the text interfaces are relatively simple.
   -  Is one interface more general-purpose than another? 
   -  Does one interface enable a more efficient implementation than another? In the text example, the character-oriented approach is likely to be significantly slower than the others, because it requires a separate call into the text module for each character.

 > Once you have compared alternative designs, you will be in a better position to identify the best design. 
 - The best choice may be one of the alternatives, or you may discover that you can combine features of multiple alternatives into a new design that is better than any of the original choices.

 > Sometimes none of the alternatives is particularly attractive; when this happens, see if you can come up with additional schemes. Use the problems you identified with the original alternatives to drive the new design(s).
  - If you were designing the text class and considered only the line-oriented and character-oriented approaches, you might notice that each of the alternatives is awkward because it requires higher level software to perform additional manipulations.
    - In order to eliminate the additional text manipulations, the text interface needs to match more closely the operations happening in higher level software.

 > The *design-it-twice principle* can be applied at many levels in a system. 
 - The most important things are simplicity and performance. It's also useful to explore multiple designs at higher levels in the system
   - such as when choosing features for a user interface, or when decomposing a system into major modules.
   - In each case, it's easier to identify the best approach if you can compare a few alternatives.

 > Designing it twice doesn't need to take a lot of extra time. For a smaller module such as a class, you may not need more than an hour or two to consider alternatives.
 - This is a small amount of time compared to the days or weeks you will spend implementing the class. 
 - For larger modules you'll spend more time in the initial design explorations, but the implementation will also take longer, and the benefits of a better design will also be higher.

 > As developers get older, they get promoted into environments with harder and harder problems. 
 - Eventually, everyone reaches a point where your first ideas are no longer good enough; if you want to get really great results, you have to consider a second possibility, or perhaps a third, no matter how smart you are.
 - The design of large software systems falls in this category: no-one is good enough to get it right with their first try

 > The *design-it-twice* approach not only improves your designs, but it also improves your design skills. The process of devising and comparing multiple approaches will teach you about the factors that make designs better or worse.
 - Over time, this will make it easier for you to rule out bad designs and hone in on really good ones.