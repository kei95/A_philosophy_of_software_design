# Chapter 8

## Pull Complexity Downwards
 >  This chapter introduces another way of thinking about how to create deeper classes.\
 > Suppose that you are developing a new module, and you discover a piece of unavoidable complexity.
 - If the complexity is related to the functionality provided by the module, then
   - handle the complexity internally within the module?
   - Most modules have more users than developers, so it is better for the developers to suffer than the users.
 - ***it is more important for a module to have a simple interface than a simple implementation.***

 > As a developer, it’s tempting to behave in the opposite fashion: solve the easy problems and punt the hard ones to someone else. If a condition arises that you’re not certain how to deal with, the easiest thing is to throw an exception and let the caller handle it.
 - If you are not certain what policy to implement, you can define a few configuration parameters to control the policy and leave it up to the system administrator to figure out the best values for them.

 > Approaches like these will make your life easier in the short term, but they amplify complexity, so that many people must deal with a problem, rather than just one person.
 - For example, if a class throws an exception, every caller of the class will have to deal with it. If a class exports configuration parameters, every system administrator in every installation will have to learn how to set them.

## 8.2 Example: configuration parameters
 > Configuration parameters are an example of moving complexity upwards instead of down. Rather than determining a particular behavior internally, a class can export a few parameters that control its behavior, such as the size of a cache or the number of times to retry a request before giving up.\
 > Users of the class must then specify appropriate values for the parameters. Configuration parameters have become very popular in systems today; some systems have hundreds of them.
 - Advocates argue that configuration parameters are good because they allow users to tune the system for their particular requirements and workloads.
    - In some situations it is hard for low-level infrastructure code to know the best policy to apply, whereas users are much more familiar with their domains.

 > However, configuration parameters also provide an easy excuse to avoid dealing with important issues and pass them on to someone else.
 - it’s difficult or impossible for users or administrators to determine the right values for the parameters. 
   - In other cases, the right values could have been determined automatically with a little extra work in the system implementation.
 - Consider a network protocol that must deal with lost packets. If it sends a request but doesn’t receive a response within a certain time period, it resends the request.
    - One way to determine the retry interval is to introduce a configuration parameter. However, the transport protocol could compute a reasonable value on its own by measuring the response time for requests that succeed and then using a multiple of this for the retry interval.
    - This approach pulls complexity downward and saves users from having to figure out the right retry interval.
    - It has the additional advantage of computing the retry interval dynamically, so it will adjust automatically if operating conditions change. 
      - In contrast, configuration parameters can easily become out of date. Thus, you should avoid configuration parameters as much as possible.

 > Before exporting a configuration parameter, ask yourself: ***“will users (or higher-level modules) be able to determine a better value than we can determine here?”***
  - When you do create configuration parameters, see if you can compute reasonable defaults automatically, so users will only need to provide values under exceptional conditions.
 - Ideally, each module should solve a problem completely; configuration parameters result in an incomplete solution, which adds to system complexity.

 ## 8.3 Taking it too far
  > Use discretion when pulling complexity downward; ***this is an idea that can easily be overdone.***
  - An extreme approach would be to pull all of the functionality of the entire application down into a single class, which clearly doesn’t make sense.
 - Pulling complexity down makes the most sense in the following cases:

 ### A
 - the complexity being pulled down is closely related to the class’s existing functionality

### B
 - pulling the complexity down will result in many simplifications elsewhere in the application

### C
 - pulling the complexity down simplifies the class’s interface. Remember that the goal is to minimize overall system complexity.

 ## 8.4 Conclusion
 - When developing a module, look for opportunities to take a little bit of extra suffering upon yourself in order to reduce the suffering of your users.
