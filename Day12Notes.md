## Lecture 12
### 2/27/2023

## Overview
This document is the lecture 12 (2/27/2023) notes for CS340: Software Engineering. This day of lecture discuses measuring quality of tests, test suite quality metrics, and the topics that will be covered in Exam 1. 
___

## Measuring Quality of Tests
* Tests only allow us to draw conclusions about the lines of code that get eexecuted
  -> How much of this exists?
* Our goal with a test suite: all of the code / requirements should be covered (checked) by the test suite
* Code Coverage - how much code is executed by a test suite?
  -> Coverage metrics tackle this definition in different ways
* Statement Coverage - fraction of source code statements that are executed by the test suite
  -> Line coverage
 - observation: if we never test line x, then testing cannot rule out the presence of a bug on x
  -> Note: you could cover line x & still have a bug
 - ex) 
 -     def foo(a,b):
 -      return a / b
 -     TEST: foo(6,2) == 3
 -           foo(6,0) -> crash!
 - even with 100% lline coverage, there could be bugs the test suite fails to expose
* All things being equal, if test A visits lines 1&2 and test B visits 1,2,3,4,
  which test do we perfer?
    - test B -> coveres more lines
* What assumptions are we making?
 - we gain the same amount of confidence (or info) we gain per line visited
___

## Test Suite Quality Metrics
* A test quite quality metric assesses the quality of a test suite (with respect to an external notion of utility) and allows test suites to be compared
* Line coverage -> one such quality metric
 - given two test suites that both run in the provided resource budget, prefer the one with higher line coverage
  -> good for decision making
* How do we measure line coverage?
 - set a breakpoint & step through (manually write down)
 - print "stuff" -> insert a print statement for each line of code
  -> slow down execution, manual effort to insert, observer effect
 - Coverage Instrumentation -> program will be automatically modified to track coverage while minimizing observer effect
 - "Solved problem" -> python coverage, gcc gcov
___

## What can go wrong with line coverage
 - 100% line coverage and still have bugs
 - state or sequencing of execution that still produces bugs
 - Implicit control flow: -> "hidden" if statement
  - ex)
  -     return a / b -> 
  -     if b != 0:
  -       return a / b
  -     else:
  -       abort
  - ex)
  -     print(ref.field) -> 
  -     if ref != null:
  -       print(ref.field)
  -     else:
  -       abort
* Interesting test cause implicit or explicit changes of control
  -> cause different branches of conditional statements to execute
* Might reduce to covering all branches
* Branch coverage - total number of conditional branches executed / covered by a test suite
  - if true   
  - if false 
  - The 'if true' case and 'if false' case are covered separately.
___

## Exam 1
* Written Exam
* Allowed one 8.5x11 piece of paper for reference notes
* Topics
  - Software vs Programs
  - Time allocation to various SE tasks
  - Linux / command line -> typical program
    - loops / conditions, file paths, scripting (shebang / permissions), text editors
  - Version control systems
    - centralized vs distributed, deltas vs snapshots, git basics (staging), working directories, 
    commit histories, branching/tags/head, rebasing vs merging, remote/PRs/forks, commit messages
  - Quality Assurance Testing
    - Internal vs External, Rice's Theorem & limit of assessment, unit testing, system integration, 
    load, test driven development, test cases & parts, mocking
## Something Fun
Good Luck Studying for Exam 1!
<p><a href="https://giphy.com/gifs/studiosoriginals-J1YFTAeTT3UAxnl6Bx">via GIPHY</a></p>
