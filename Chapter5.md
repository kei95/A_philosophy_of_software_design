# Chapter 5

## Information Hiding(and Leakage)
 > Chapter 4 argued that modules should be deep. This chapter, and the next few that follow, discuss techniques for creating deep modules.

## 5.1 Information hiding
 > The most important technique for achieving deep modules is information hiding. This technique was first described by David Parnas.\
 - The basic idea is that each module should encapsulate a few pieces of knowledge, which represent design decisions
 - The knowledge is embedded in the module's implementation but does not appear in its interface, so it's not visible to other modules.

 > Information hiding reduces complexity in two ways.
 ### First
 - it simplifies the interface to a module. The interface reflects a simpler, more abstract view of the module’s functionality and hides the details
    - this reduces the cognitive load on developers who use the module.

### Second
 - Second, information hiding makes it easier to evolve the system.
   - If a piece of information is hidden, there are no dependencies on that information outside the module containing the information, so a design change related to that information will affect only the one module.

 > When designing a new module, you should think carefully about what information can be hidden in that module.\
 > If you can hide more information, you should also be able to simplify the module’s interface, and this makes the module deeper.
 - Note: hiding variables and methods in a class by declaring them private isn’t the same thing as information hiding.
   - Private elements can help with information hiding, since they make it impossible for the items to be accessed directly from outside the class.
   - However, information about the private items can still be exposed through public methods such as getter and setter methods. When this happens the nature and usage of the variables are just as exposed as if the variables were public.

 > The best form of information hiding is when information is totally hidden within a module, so that it is irrelevant and invisible to users of the module.\
 > However, partial information hiding also has value.
 - For example, if a particular feature or piece of information is only needed by a few of a class’s users, and it is accessed through separate methods so that it isn’t visible in the most common use cases, then that information is mostly hidden.
   - Such information will create fewer dependencies than information that is visible to every user of the class.

## 5.2 Information leakage
 > The opposite of information hiding is ***information leakage.***\
 > Information leakage occurs when a design decision is reflected in multiple modules. This creates a dependency between the modules
 - any change to that design decision will require changes to all of the involved modules.

 > If a piece of information is reflected in the interface for a module, then by definition it has been leaked; thus, simpler interfaces tend to correlate with better information hiding. However, information can be leaked even if it doesn’t appear in a module’s interface.
 - However, information can be leaked even if it doesn’t appear in a module’s interface.
   - Suppose two classes both have knowledge of a particular file format (perhaps one class reads files in that format and the other class writes them). Even if neither class exposes that information in its interface, they both depend on the file format: if the format changes, both classes will need to be modified.
 - Back-door leakage like this is more pernicious than leakage through an interface, because it isn’t obvious.

 > Information leakage is one of the most important red flags in software design. One of the best skills you can learn as a software designer is a high level of sensitivity to information leakage.
 - If you encounter information leakage between classes, ask yourself “*How can I reorganize these classes so that this particular piece of knowledge only affects a single class?*”
    - If the affected classes are relatively small and closely tied to the leaked information, it may make sense to merge them into a single class.
 - Another possible approach is to pull the information out of all of the affected classes and create a new class that encapsulates just that information.
    - However, this approach will be effective only if you can find a simple interface that abstracts away from the details

 ## RED FLAG: Information Leakage
 - Information leakage occurs when the same knowledge is used in multiple places, such as two different classes that both understand the format of a particular type of file.

## 5.3 Temporal decomposition
 > One common cause of information leakage is a design style I call ***temporal decomposition***\
 > In temporal decomposition, the structure of a system corresponds to the time order in which operations will occur.
 - Consider an application that reads a file in a particular format, modifies the contents of the file, and then writes the file out again.
    - With temporal decomposition, this application might be broken into three classes: one to read the file, another to perform the modifications, and a third to write out the new version. Both the file reading and file writing steps have knowledge about the file format, which results in information leakage.
    - The solution is to combine the core mechanisms for reading and writing files into a single class. This class will get used during both the reading and writing phases of the application.

 > Order usually does matter, so it will be reflected somewhere in the application. However, it shouldn’t be reflected in the module structure unless that structure is consistent with information hiding (perhaps the different stages use totally different information).
 - **When designing modules, focus on the knowledge that’s needed to perform each task, not the order in which tasks occur.**

 ## RED FLAG: Temporal Decomposition
 - In temporal decomposition, execution order is reflected in the code structure: operations that happen at different times are in different methods or classes. If the same knowledge is used at different points in execution, it gets encoded in multiple places, resulting in information leakage.

## 5.4, 5.5 Example HTTP server
 > The students in the course were asked to implement one or more classes to make it easy for Web servers to receive incoming HTTP requests and send responses(See figure 5.1 below).

 ## Figure 5.1
![image info](./images/Figure5-1.png)

 > The most common mistake made by students was to divide their code into a large number of shallow classes, which led to information leakage between the classes.
 - One team used two different classes for receiving HTTP requests; the first class read the request from the network connection into a string, and the second class parsed the string.
    - This is an example of a temporal decomposition (“first we read the request, then we parse it”).
 - Because the classes shared so much information, it would have been better to merge them into a single class that handles both request reading and parsing. This provides better information hiding, since it isolates all knowledge of the request format in one class, and it also provides a simpler interface to callers (just one method to invoke).
    - This example illustrates a general theme in software design: information hiding can often be improved by making a class slightly larger.

 > One reason for doing this is to bring together all of the code related to a particular capability (such as parsing an HTTP request), so that the resulting class contains everything related to that capability.


 ## RED FLAG: Temporal Decomposition
 - If the API for a commonly used feature forces users to learn about other features that are rarely used, this increases the cognitive load on users who don’t need the rarely used features.

## 5.8 Information hiding within a class
 - Try to design the private methods within a class so that each method encapsulates some information or capability and hides it from the rest of the class.
 - In addition, try to minimize the number of places where each instance variable is used.
    - Some variables may need to be accessed widely across the class, but others may be needed in only a few places; if you can reduce the number of places where a variable is used, you will eliminate dependencies within the class and reduce its complexity.

## 5.9 Taking it too far
 > Information hiding only makes sense when the information being hidden is not needed outside its module.\
 > If the information is needed outside the module, then you must ***not*** hide it.
 - Suppose that the performance of a module is affected by certain configuration parameters, and that different uses of the module will require different settings of the parameters.
    - In this case it is important that the parameters are exposed in the interface of the module, so that they can be turned appropriately.
 - it’s important to recognize which information is needed outside a module and make sure it is exposed.

## 5.10 Conclusion
 - Information hiding and deep modules are closely related. If a module hides a lot of information, that tends to increase the amount of functionality provided by the module while also reducing its interface. This makes the module deeper.\
 - Conversely, if a module doesn’t hide much information, then either it doesn’t have much functionality, or it has a complex interface; either way, the module is shallow.
 - When decomposing a system into modules, try not to be influenced by the order in which operations will occur at runtime;
    - that will lead you down the path of temporal decomposition, which will result in information leakage and shallow modules.
    - Instead, think about the different pieces of knowledge that are needed to carry out the tasks of your application, and design each module to encapsulate one or a few of those pieces of knowledge. This will produce a clean and simple design with deep modules.
