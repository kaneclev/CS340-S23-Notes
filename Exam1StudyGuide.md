# Exam 1 Study Guide
## For exam on 01/03/2023

# Overview
This file reviews the concepts and ideas covered from the beginning of the semester to 3/1/23. The document follows the format we followed in the class prior to the exam. First off all the topics we covered are listed and then it delves into more specific info, such as relevant commands. 

## Topics
- Software vs. programs
- Time allocation to various SE tasks
- Linux / command line
    - typical program / commands
    - loops / conditions
    - file path (`basename`' & `dirname`' commands)
    - scripting (shabang / permissions)
    - text editors (nano and vim)
- Version Control Systems
    - centralized vs. distributed
    - deltas vs. snapshots
    - get basics → staging & working directory
    - commit histories
    - branching, tags, head
    - rebase, merge
    - remote / pull requests / forks
    - commit messages best practices
- Quality Assurance & Testing
    - internal vs. external quality
    - rice's theorem & limits of assessment 
    - unit, system, integration, and load testing
    - test driven development
    - test cases 
    - mocking

## Notes

_Software vs. Programs_

> ### Definition
>Program - Collection of instructions or ordered operations for a computer to preform a function or task

>### Definition
>Software - Collection of programs procedures, data, or instructions that work together to provide a specified functionality

- Similarities and differences:
    - similarities: programming languages, coding
    - differences: public, size, security, usability, quality control

_Time allocation to various SE tasks_

- 70 - 90% of the budget / time is spent on maintenance

_Linux / command line_
- typical program / commands_
- _loops / conditions_
- _file path (`basename`' & `dirname`' commands)_
- _scripting (shabang / permissions)_
- _text editors (`nano`' and `vim`')_


- Command lines give access to run tools under the hood
- Shell is a program that exposes an OS' services to a human user or other programs
- A shell script is a text file containing commands for a shell to execute
    - The first line starts with a "shabang" or `#!/bin/bash`'
- Useful commands:
    - `chmod`': a command to change permissions
        - `chmod +x \<file>`': is used to make a file executable
    - `ls`': list the content in a directory
    - `pwd`': present working directory
    - `cd`': change directory
    - `curl`': transfer from URL
    - `mkdir`': make directory
    - `less`': open file
    - `man`': help manual
    - `ssh`': secure shell, allows remote access to shell on another computer
    - `basename`': extracts only the file name
    - `dirname`': extracts only the file path
    - `|` (pipe): take output from one program as input to a second program
    - `xargs`': popes but as command line arguments
    - `cut`': delimiter to break up lines
    - `wc`': word count

___
- For loop: 
```
for i in {0..100}
    do
    ...
    done
```
- Conditionals:
```
if [-f name]
    then
        ...
    else
        ...
fi
```
    - `f`' is used for files
    - `d`' is used for directories
    - `z`' is to check for empty files

____
- Redirecting
    - `'\>`': overwriting the target file
    - `'\>>`': appends to the target file
    - `2>`': sends the error output
    - `1>`': sends the standard output

- Text editors: nano, vi(m), emacs
    - vi commands:
        - `i;`' insert mode
        - `':q!`' force quit, no ! for quit
        - `':w`' write the file
        - \<escape> leave insert mode

- _Version Control Systems_
    - _centralized vs. distributed_
    - _deltas vs. snapshots_
    - _git basics → staging & working directory_
    - _commit histories_
    - _branching, tags, head_
    - _rebase, merge_
    - _remote / pull requests / forks_
    - _commit messages best practices_

- Dominant activity of software development is maintenance
- Version control systems allow modifying files, mark files as ready to contribute, and bundle and share changes to everyone.
- Version control systems simplify maintaining code
- Centralized systems:
    - 1 unified history
    - everyone agrees  on versions available 
    - client must have a set of working files
    - to commit revisions a user must connect to the main server
- Distributed system:
    - shared history
    - redundancy → multiple copies of history
    - client makes copy on own system
    - client check in / commits to their own history 
    - potential for disagreement, so there must be a way to resolve conflicts and sync histories
- Encoding the history of a repository:
    1. Deltas: track the changes (deltas) and save those changes
    2. Snapshots: keep full copies of changed files while the unchanged files are pointers to previous versions
- Git workspace has 3 states / locations:
    1. Working directory
    2. Staging
    3. Repository
- History of a repository forms a tree
    - Committing is inserting a new node
- Head: marks our working directory
- Hashes create unique IDs for each commit
- Branches are additional labels to keep track of parts and version history
- Tags are permeant label or nickname on a commit 
- Recombining branches 
    1. `merge`: combine commits & form a new commit with combined changes (two parents)
    2. `rebase`: "copy" the commits into another branch - like a transplant
- Commits:
    - message should describe problem being solved or features being added
        - can reference a bug report but should stand alone
    - don't want to assume access to outside resources
    - describe changes being done
    - first line of the message should be the subject
    - message should wrap at 72 or 80 characters
    ` nano -r 72`
- Dos and Don'ts:
    - don't mix whitespace / formatting with functional changes
    - don't mix unrelated functional changes
    - don't submit all code with one commit
    - do try to keep commits small & modular
- Git
    - git is a distributed version control system
    - connect a repo to another copy of the repo specify by ` git remote -v `
    - Sync commands:
        1. `git fetch`: download new commits from remote
        2. `git merge`: combine downloaded commits with local history 
        3. `git pull`: does both the operations of a fetch and merge commands
        4. `git push`: upload our new commits to the remote
    - all remote branches are prefixed with the remote in the name
        - example: `hans/main`
    - general rule:
        1. `rebase`' unshared changes
        2. `merge`' with shared changes
    - pull requests: request for developer to pull your commits to upstream repo
        1. Assign yourself an issue / bug report 
        2. Fork/clone the repo
        3. Make branch for the fix
        4. Commit to the new branch
        5. Push to the fork
        6. Open a full request

Git commands from Learn Git Branching
____

```
git commit 
git branch
git checkout
git merge
git rebase
git reset
git revert
git clone
git fetch
git pull
```
____

- _Quality Assurance & Testing_
    - _internal vs. external quality_
    - _rice's theorem & limits of assessment_
    - _unit, system, integration, and load testing_
    - _test driven development_
    - _test cases_
    - _mocking_

- Developers want to deliver high quality software at low cost

>### Definition 
> Quality Assurance - The maintenance of desired level of quality in a service or product, especially by means of attention to every stage of the delivery or production

- Two types of quality
    1. External: customer facing, essentially does the software do the right thing
    2. Internal: source code is readable, well document, maintainable
- Internal quality is mostly about maintainability
    - human code review
    - code analysis tools (linters)
    - - use programming idioms & design standards
    - follow local coding standards
- Rice's Theorem: prevents programs from always giving the right answer, all non-trivial semantic properties are undecidable
    - x is not always wrong, but not always right
- We approximate correctness with type checkers, linters, static analysis
- Software testing is an investigation conducted to provide stakeholder with information about quality of software
- Testing gives confidence that your implementation adheres to specification
- An oracle is the source of sample  output for test cases
- System testing: test end-to-end system for correctness 
- Regression testing: try to see regression in the source code
- Unit testing: test chunks of code
    - frameworks: JUnit, Python unittest
- Test cases:
    1. Establish some condition
    2. Preform an operation
    3. Assert post condition
    - each test case should be run in a "fresh environment"
- Test fixture: surrounds a test case to provide code that is run before and after each test case
- Unit testing discover: python3 -m unittesting discovery
- Test driven discover:
    1. Write a test to add a new feature 
    2. Write code that the unit test is testing for
    3. Run all available tests
- Integration testing: one layer up from unit, do the chunks work well together?
- Challenges of testing:
    1. Different hardware configurations
    2. What if the tool is broken? (test is broken)
    3. Cost / speed (external APIs)
- Mocking: using mock objects (simulated objects) that mimic the behavior of real objects in a controlled way
    - cash test dummies, sometimes called stubs
- Functional properties: correct solution
- Non-functional properties:  memory, runtime, security, power, performance with many users
- Load testing: how does the system respond under typical usage
    - stress test → test under extreme usage
- Testing & QA  is about 25-35% of IT budgets

- Measuring quality of tests: 
    - code coverage: how much code is executed by the test suite
    - statement coverage: fraction of source code statements that are executed by test suite → loosely the same as line coverage
    - test suite quality metrics asses the quality of a test suite (with respect toe external notion o futility) and allows test suites to be compared
        - line coverage is on such metrics
    - how do we measure line coverage?
        - coverage instrumentation programs that auto modify code to track coverage, such as `python coverage` or `gcc gcov`
    - implicit control flow: hidden if statements
    - interest test cases cause implicit or explicit changes of control → causes different branches of conditionals to execute
    - branch coverage: total number of conditional branches covered by test suite

# Something Fun!
![Exam Meme](https://cs.uwaterloo.ca/~dtompkin/teaching/memes/cs136-w18-meme-09.jpg "Funny pic")
