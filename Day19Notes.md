# Lecture Notes For 3/29/23 - Lecture 19
## Overview
This is a continuation of the notes from 3/27 on the overview and sections of the bug life cycle and an introduction into fault localization. 

---

## **Bug life Cycle Continued ->**

### 3) Assignment

>#### Definition
>#### Assignment Definition -> Who should fix this bug.

One should  ***Associate / Assign*** a developer or team with addressing the bug report.

**Ways to assign bug reports**
* Random Assignment 
* User Self Select -> Distributed System.
* Manager assigns -> Centralized System.
* Manual Assignment -> State of the art version.


All of these assignments are based on the idea of "Ownership". But how do we determine who the owner is?? Is it...

* Based on the last person to edit the file?
* The person who created the file?

---
### 4) Bug resolution

>#### Definition
>#### Resolution Definition -> Result of the most recent effort to address it.
*This is not the same as "fixed" because there are other possible outcomes.*

How many reports end up with a duplicate resolution?? 

---
### 5) Send to Quality Assurance
We did not go into any more depth on this subsection.

---

### 6) Reopened
Evidence that suggests our prior resolution was insufficient.

* Quality Assurance Rejects.
* Regression.
* More user reports.
* No longer out of scope.
* Required changes have been made.

---
## **Debugging ->**
What is the most frustrating part of debugging?

* Revealing new bugs while fixing one bug.
* Manually debugging.
* Finding the actual bug.
* Time Consuming.

>#### Definition
>#### Fault Localization -> The task of identifying source code regions implicated with  a bug.
If regression test is failing which lines should we change to resolve this failing test?

How do we debug?
* Step through the program?
* With debugger?
* With Prints?

Confounding Factors
1. Localization is not typically unique
    * Many places for a bug to exist.
    * Example -> null/none check before/after calling a function. 
2. Code Size 
    * Googles Codebase is 2000000000 lines Vs Libpng 85000 lines.

    Example -> Lets say there is a bug somewhere in Libpng that you can find in 1 minute. 
    2000000000 lines $*{1 \text{ min} \over 85000 \text{ lines} }$ = 23529 minutes = 16 days 8 hours and 9 minutes.

We need an **automated** approach to filter code so we can look at a small excerpt.

Could we use smoe knowledge from quality assurance to help? 

If we dont test line x, then we dont know anything about it. 
Filter out all lines that are not covered. Passing tests give confidence in covered lines. Failing tests reduce confidence in covered lines. The ranking of lines in a program by coverage is called *Spectrum Based Fault Localization*.

---
## Something Fun!

![Alt Text](https://preview.redd.it/8359mllhg8k41.jpg?auto=webp&s=95094f7a3b0677d002ea9f2e5e1b560a628a7ad0 "Funny pic")






 


