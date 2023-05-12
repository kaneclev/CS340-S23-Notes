# Lecture 6 - 2/6/2023
Catya Temkin

## Overview ##
In this lecture, we discussed Version Control Systems and useful related git commands. I will go more in depth with
Centralized Systems versus Distributed Systems along with their pros and cons.

## Version Control Systems
- Simplify maintaining code 

### Centralized Systems 
![centralized system diagram](https://www.htown-tech.com/uploads/6/9/4/9/69493533/centralized-vs-distributed-version-control-system-2_orig.jpg)

- There is **one** unified history 
    - everyone has to agree on avalible versions
    - clients just have a set of "working" files
    - to commit changes, client must reconnect to the main server  
- Pros:
    1. Possible to look at past versions 
    2. Simplicity of a single server 
- Cons:
    1. Single server may go offline 
    2. Must be connected to server to commit (need access to internet)

### Distributed Systems
![distributed system diagram](https://www.htown-tech.com/uploads/6/9/4/9/69493533/centralized-vs-distributed-version-control-system-3_orig.jpg)

- Shared history
    - Clients make a copy of the systems history when checking out code
    - Clients check in/commits to their personal history 
- Pros:
    1. No need for internet to commit 
    2. No problem if server goes offline
- Cons:
    1. Redundancy (multiple copies of history)
    2. Potential for disagreement 
        - need way to resolve conflicts and share histories 
- Git is a distributed verson control system 
### Encoding the History of a Repository
- track the changes (delta)
    - can use tools called diff and patch
- **snapshots** are full copies of changed files
    - unchanged files are pointers to the previous version
- Git uses snapshots 
- The Git workspace has **3** different states/loactions
    1. Working directory 
    2. Staging 
    3. Repository (history)
- Useful and related Git commands
    - `status` view current status 
    - `log` sequence and information of past commits 
    - `add` move from working directory to staged
    - `restore --staged` move from staged back to working directory
    - `git commit` move from staged to repository
    - `reset --soft HEAD^` undo commit
    - `checkout` move from repository to working directory

## Meme of the day
![Something Fun](https://iamskb258154309.files.wordpress.com/2020/07/c7ded-1qdejjdxa0orhqnkkmjmytg.jpeg)
