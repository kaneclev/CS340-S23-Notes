## **Day 11 Notes : New Testing Metrics**
#
### Overview
#
Today we learn more about unit testing and it's benefits and challenges. While also exploring  new testing metrics that we can use to ensure the best quality of the programs we maintain. 

***

### _Unit Testing_
#
>**Unit Testing** is when you test  indivual chunks of source code to determine that it works in isolation from the rest of the program. 

### Advantages of Unit Testing

It is in smaller chunks so it's easier to see whether a bug could be coming from that block.

Because it is small, unit testing becomes faster and more frequently.
Can support Test Driven Development.

### Test Driven Development

>**Test Driven Development**
is when you write the test file before you even write the new feature. 
 + Write a unit test for a new feature.
    + Your test will fail at this point.
+ Write code that the unit test are testing for. 
+ Run all available unit test. 
+ Fix any regressions. 

Now go back and implement the new feature. 
***
### New Testing Metrics
#

 While Unit Testing is great, it fails at seeing how things work together.

 What happens when we combine unit tested features into a larger program?
> **Integration Testing** is one step ahead of unit testing because individual software modules are combined and tested as a group.

This is one level up from unit testing.

Going a step further: 

>**System Testing** is end to end integration testing. We evaluate how the various components of an application interact together in the full, integrated system or application.

The difference here is abstraction. 

>**Load Testing** is testing that caluates how does a system preform under typical resource usage. 

(typical users, request/hour, etc...)
>**Stress Testing** is to see how far we can push a program until it breaks. 

---

### Challenges of Testing
#

_How do we work around challenges?_
different hardware configurations

What if the tool is broken?

What if the _test_ is broken?

>**Mocking** is a common tool in software engineering when it comes to this challenge. Mocking is used to simulate objects that mimic the behavior of real objects in a controlled way. 

i.e. crash dummies

In software, these mock objects are sometimes also called **stubs**. 

>**Stubs** are bits of code with some interdace as the real code but return dummy data

**Example 1**

Web app that uses chat bot for interactions

Issue: API could still be under development or cost per quary

Solution: write stubs that return hardcoded results

 **Example 2**

Code where certain kinds of failures might happen sporadically (disk full, condition dropped, corruption)

Issue: errors " don't happen" in development

Solution: use testing frameworks/mocking frameworks that can trigger these transcient errors

---

This brings us to our new topic for Software Engineering: **_Quality of Test and Test Suite_**

"Testing Quality Assurance accounts for 25-35% of IT budgets _(2015 -2019)_" - KA

If testing is the best way to gain confidence but is expensive, how do we ensure that we are testing in a efficent manner?

What we want is for all of the requirement to be covered or checked by test suite. 

***
### Meme
#

CS Nerd: I can't find this bug anywhere!

Mom: Why are you looking for bugs?
