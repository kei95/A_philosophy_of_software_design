# Chapter 20

## Designing for Performance
 > Up until this point, the discussion of software design has focused on complexity; the goal has been to make software as simple and understandable as possible. But what if you are working on a system that needs to be fast? How should performance considerations affect the design process? This chapter discusses how to achieve high performance without sacrificing clean design. The most important idea is still simplicity: not only does simplicity improve a system’s design, but it usually makes systems faster.

 ## 20.1 How to think about performance
 > The first question to address is "how much should you worry about performance during the normal development process?". If you optimize every statement for maximum speed, it will slow down development and create a lot of unnecessary complexity. Further more, many of the "optimizations" won't actually help performance. 
 - In this "death by a thousand cuts" scenario it's hard to come back later and improve the performance, because there's no single improvement that will have much impact.

 > The best approach is between these extremes, where you use basic knowledge of performance to choose design alternatives that are "naturally efficient" yet also clean and simple. They key is to develop an awareness of which operations are fundamentally expensive. Here are a few examples of operations that are relatively expensive today:
 - Network communication: even within a datacenter, a round-trip message exchange can take 10–50 µs, which is tens of thousands of instruction times. Wide-area round-trips can take 10–100 ms.
 - I/O to secondary storage: disk I/O operations typically take 5–10 ms, which is millions of instruction times. Flash storage takes 10–100 µs. New emerging nonvolatile memories may be as fast as 1 µs, but this is still around 2000 instruction times.
 - Dynamic memory allocation (*malloc* in C, new in C++ or Java) typically involves significant overhead for allocation, freeing, and garbage collection.
 - Cache misses: fetching data from DRAM into an on-chip processor cache takes a few hundred instruction times; in many programs, overall performance is determined as much by cache misses as by computational costs.

 > The best way to learn which things are expensive is to run micro-benchmarks(small programs that measure the cost of a single operation in isolation). Once you have a general sense for what is expensive and what is cheap, you can use that information to choose cheap operations whenever possible. In many cases, a more efficient approach will be just as simple as a slower approach.
 - e.g. storing a large collection of objects that will be looked up using a key value, you could use a hash table or an ordered map. Both are commonly available in library packages, are both are simple and clean to use. However, hash tables can easily be 5-10x faster.
   - Thus, you should always use a hash table unless you need the ordering properties provided by the map.

 > If the only way to improve efficiency is by adding complexity, then the choice is more difficult. If the more efficient design adds only a small amount of complexity, and if the complexity is hidden, so it doesn't affect any interfaces, then it may be worthwhile(but beware: complexity is incremental). 
 - If the faster design adds a lot of implementation complexity, or if it results in more complicated interfaces, then it may be better to start off with the simpler approach and optimize later if performance turns out to be a problem.
   - However, if you have clear evidence that performance will be important in a particular situation, then you might as well implement the faster approach immediately.

 > In general, simpler code tends to run faster than complex code. If you have defined away special cases and exceptions, then no code is needed to check for those cases and the system run faster. Deep classes are more efficient than shallow onces, because they get more work done for each method call. Shallow classes result in more layer crossings, and each layer crossing adds overhead.

  ## 20.2 Measure before modifying
  > But suppose that the system is still too slow, even though you have designed it as described above. It's tempting to rush off and start making performance tweaks, based on your intuitions about what is slow. ***Don't do this!*** Programmers' intuitions about performance are unreliable.
  - This is true for experienced developers. If you start making changes based on intuition, you'll waste time on things that don't actually improve performance, and you'll probably make the system more complicated in the processes.

  > Before making any changes, measure the system's existing behavior. This serves two purposes.
  - First, the measurements will identify the places where performance tuning will have the biggest impact. It isn't sufficient just to measure the top-level system;
    - This may tell you the system is too slow, but it won't tell you why. You'll need to measure deeper to identify in detail the factors that contribute to overall performance;the goal is to identify a small number of very specific places where the system is currently spending a lot of time, and where you have ideas for improvement
 -  The second purpose of the measurements is to provide a baseline, so that you can re-measure performance after making your changes to ensure that performance actually improved.
    - If the changes didn't make a measurable difference in performance, then back them out(unless they made the system simpler). There's no point in returning complexity unless if provides a significant speedup.

 ## 20.3 Design around the critical path
 > At this point, let's assume that you have carefully analyzed performance and have identified a piece of code that is slow enough to affect the overall system performance. The beat way to improve its performance is with a "fundamental" change, such as introducing a cache, or using a different algorithmic approach(balanced tree vs. list, for instance). If you can identify a fundamental fix, then you can implement it using the design techniques discussed in previous chapters.
 - Unfortunately, situations will sometimes arise where there isn't a fundamental fix. This brings us to the core issue for this chapter, which is how to redesign an existing piece of code that it runs faster.
   - This should be your last resort, and it shouldn't happen often, but there are cases where it can make a bid difference. The key idea is to design the code around the critical path.

 > Start off by asking yourself what is the smallest amount of code that must be executed to carry out the desired task in the common case. Disregard any existing code structure. Imagine instead that you are writing a new method that implements just the critical path, which is the minimum amount of code that must be executed in the most common case.
 - The current code is probably cluttered with special cases; ignore them in this exercise. The current code might pass through several method calls on the critical path; imagine instead that you could put all the relevant code in a single method.
 - The current code may also use a variety of variables and data structures; consider only the data needed for the critical path, and assume whatever data structure is most convenient for the critical path.
   - e.g. it may make sense to combine multiple variables into a single value. Assume that you could completely redesign the system in order to minimize the code that must be executed for the critical path. Let's call this code ***"the ideal"***

 > The ideal code probably clashes with your existing class structure, and it may not be practical, but it provides a good target: this represents the simplest and fastest that the code can ever be. The next step is to look for a new design that comes as close as possible to the ideal while still having a clean structure.
 - You may have to add a bit of extra code to the ideal in order to allow clean abstractions;
   - e.g. if the code involves a hash table class. In my experience it's almost always possible to find a design that is clean and simple, yet comes very close to the ideal.

 > One of the most important things that happens in this process is to remove special cases from the critical path. When code is slow, it's often because it must handle a variety of situations, and the code gets structured to simplify the handling of all the different cases. 
 - Each special cases adds a little bit of code to the critical path, in the form of extra conditional statements and/or method calls.
 - Each of these additions makes the code a bit slower. When redesigning for performance, try to minimize the number of special cases you must check. Ideally, there will be a single *if* statement at the beginning, which detects all special cases with one test. In the normal case, only this one test will need to be made, after which the critical path can be executed with no additional test for special cases.
   - If initial test fails(which means a special case has occurred) the code can branch to a separate place off the critical path to handle it. Performance isn't as important for special cases, so you can structure the special-case code for simplicity rather than performance.

 ## 20.5 Conclusion
 - The most important overall lesson from this chapter is that clean design and high performance are compatible. The Buffer class rewrite improved its performance by a factor of 2 while simplifying its design and reducing code size by 20%. 
 - Complicated code tends to be slow because it does extraneous or redundant work.
 - On the other hand, clean and simple code will probably be fast enough that you don't have to worry much about performance in the first place.
 - In the few cases where you do need to optimize performance, the key is simplicity again: find the critical paths that are most important for performance and make them as simple as possible.