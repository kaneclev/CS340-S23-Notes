# Software Design
### *Lecture 24, 04/17/2023*
&nbsp;
## **Overview**
In lecture 24, we started thinking about software design and software design patterns. Diving into how we can design software to fit certain aspects of software development such as code review or maintainability.
___
&nbsp;
## What's the idea here?
70% to 90% of time in software development is spent on maintenance tasks. So, if you want to optimize your process of developing software to help you write new software faster, the maximum "speedup" or "imporvement" you can get is only 30%. But, we can design software to make a certain stage in the development lifecycle faster. This follows Amdahl's Law:
- [Amdahl's Law](https://en.wikipedia.org/wiki/Amdahl%27s_law) is the formula which gives the theoretical speedup of the execution of a task at fixed workload that can be expected of a system whose resources are improved.
## Design for Code Review
Since code review is reliant on code comprehension and readability, what are some things we can do to help?
- Avoid long lines of code.
- Reduce the number of variables in a region of code.
- Ensure to follow common naming patterns, for example:
  - CamelCase (java).
  - Snake_case (python).
  - Hungarian notation (lAccountNumber where "l" is for "long").
- Ensure to have ample comments and block comments/documentation.
- Have blank lines to space out code properly and keep your notation consistent by:
  - Using similar variable names.
  - Use consistent indentation.
  - Use consistent spacing between blocks of code.
## Design for Maintainability
Code is considered [*maintainable*](https://en.wikipedia.org/wiki/Maintainability) if it is organized well and is readable. Some things we can do are:
- Make it easy to change, extend, or refactor the program.
- Break the code into intepentent modules, units, or functions.
  - Avoid writing everything in your main program.
  - Avoid code duplication (two or more of the exact same lines).
- Use object oriented design:
  - Manages complexity well.
  - Allows for unit testing.
  - Breaks complex systems into simple pieces.
  - For extensibility, we want to program to [interfaces](https://en.wikipedia.org/wiki/Interface_(object-oriented_programming)):
    - Which will provide a list of functions/methods that are supported.
    - It will assume the absolute minimum about the classes we interact with.
## Software Design Patterns
So, now we've taken a look at software design usages and examples. It's time to dive into software design patters. What is a [software design pattern](https://en.wikipedia.org/wiki/Software_design_pattern) anyways?
> *A software design pattern is a general, reusable solution to a commonly-occurring problem within a given context in software design (kinda like a recipe).*

Essentially, we want to provide the best practices for problems that we've seen in the past. There is a book called "Design Patterns" by Erich Gamma, John Vlissides, Ralph Johnson, Richard Helm. The book is commonly referred to as the "Gang of Four", based off the four authors. They propose 23 different software design patterns, but for the sake of this lecture, we went over 9 of the 23 patterns:
1. Strategy Pattern.
2. Composite Pattern.
3. Factory Pattern.
4. Command Pattern.
5. Adapter Pattern.
6. Facade Pattern. 
7. Observer Pattern.
8. Iterator Pattern.
9. Visitor Pattern.

## Strategy Pattern
This pattern is based on runtime factors to choose what algorythm/strategy to use. We use this when it is possible to receive a varying input that we won't know until runtime. This pattrern allows the calling of code to be more flexible and reusable. 
- An example of the strategy pattern is a parking meter object that, given an amount of money, calculates an amount of time based on the parking costs at different times of the week.
## Composite Pattern
This pattern intends to compose objects into trees structures or boxes to represent part-whole hiearchies. Generally, this pattern is similar to the strategy pattern. Essentially, this pattern is picking a strategy to choose a strategy to use in a given context.
- For example, a parking meter object and a time of date object, which alone are two strategy patterns. The composite pattern is a parking meter, with multiple strategy patterns (fees/charges) that depend on the time of day.
## Factory Pattern 
The Factory pattern defines an interface for creating an object, but lets subclasses decide which class to instantiate. The Factory method lets a class defer instantiation it uses to subclasses. We use this on functions of methods that run defferent commands based on what input is given.
- An example is a valueOf() method which exists in String and wrapper classes, like Integer and Boolean, and used for type conversion i.e. converting String to Integer or String to double in java.
## Command Pattern
This pattern is a behavioral design pattern that turns a request into a stand-alone object that contains all information about the request. This is useful when creating GUI buttons and menu items, also for recording a sequence of actions by keeping a list of the command objects as they are executed (this will let you "play back" the same sequence). The motivation for using this pattern is that the executor of the command does not need to know anything at all about what the command is, what context information it needs on, or what it does (this is all encapsulated in the command).
- An example of this is a check at a restaurant. The waiter takes an order (command) from a customer which goes on the check, the order is then queued for cooking, the check pads are not dependent to a specific menu, so many things can be cooked. The order encapsulated different things inside to execute, which is executed by the cook. The cook then returns the result of the order which the waiter brings back to the customer.
## Adapter Pattern
The Adapter pattern is essentially a class that allows two non-compatible classes to work together or to interface together. This is useful when we want to use an existing class, but the interface doesn't match the one we need. This is also useful when we want to create a reusable class that works with an unrelated class which don't necessarily have compatible interfaces. This pattern is great for improving the resuability of older code or older aspects of a program. It also allows for seperation of concerns and allows your development of a program to be more seamless.
- A breif example of the Adapter pattern is a cell phone dongle connector (9mm headphone jack to lightning port). 
## Facade Pattern
The Facade pattern is one class that encapsulates a handful of classes for simplifying them or making them easily readable. We use this pattern when we want to provide a simple interface to a complex solution for simplification and readability. It is also useful when there are many dependencies between classes of an abstraction (interface). The motivation to use this pattern is that it provides a simple single interface to work with and it shields its users from subcomponents.
- For example, the Facade pattern is used in intrographics, which we learned in CS-140.
## Observer Pattern
The Observer pattern is where we use an object to maintain a list of dependents and notifies them automatically if any state changes (usually by calling one of their methods). This is often used for implementing event-handeling systems in event-driven software. The Observer pattern allows us to update the information of something in tandem with the event happeneing. 
- An example of this is taking a keyboard input(s) and handing each input line as its own seperate "event".
## Iterator Pattern
The Iterator pattern let's us traverse elements of a collection or data structure without exposing its underlying representation. We use this when we want to iterate through elements in different data structures. This is beneficial when we need to easily access elements in a collection. 
- For example, we can have different iterator objects for traversing trees which encapsulates traversal details. Different iterator objects could represent things like depth-first traversal, breadth-first traversal, or level order traversal.
## Visitor Pattern
The Visitor pattern allows us to define and add new functions or methods to object structures without modifying the code of the structure. We want to use this pattern when we want to define a new operation over a structure that is rarely changed or is unchangable. The motivation of using this is the ability to easily add new operations to complex data structures. 
- An example of this is a set of classes that have two different interfaces and we want a function that can be used for any class in the set. Define a Visitor class with methods to be used anywhere in the class structure.