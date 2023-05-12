# Lecture 7 Notes
## 2/8/23

---
## Overview
This lecture focuses on the basics of git, including tags, branches, merges,
and rebases, as well as how to write a good commit message. Tags and branches 
are labels used to keep track of important commits within a repository, and merges 
and rebases are ways to organize branches and commits.

---
## Working With Git
The history of a repository forms a tree, or an acyclic graph, where 
there is a linear, unique shortest path from the the root to any 
node (commit) in the tree. Since each node is a 'commit,' then at any
point in time, our working directory is based on some node in the tree.

So when we **commit**, we insert a new node, which become a child of 
the commit the current working directory was based off of. This means we 
need a way of marking the node or commit that the working directory is based 
off of. This is done with the **HEAD** pointer. 

One benefit of git is that we should be able to randomly access any commit 
in the tree. To do this, each commit gets a unique identifier that we call 
its **hash**. Hashes are a fixed length value and represent the data.

We can **checkout** a commit to open up the version of the reposititory when 
the commit was made. We do this with the command:

 `git checkout <commit_hash>`

For convenience, we can make additional labels besides the **HEAD** in 
order to keep track of parts of the version history. We can do this 
with **branches** and **tags**.

---
## Tags
When we apply a tag to a commit. It will act like a permanent label 
for that commit. We can add a tag at the current head with:

 `git tag <tagname>` 

or at a specified commit with:

`git tag <tagname> <commit_hash>`

![Alt text](git%20tag%20(2).png)

When we'd like to look at a specific commit, we can **checkout** that 
commit with:

`git checkout <commit_hash>`

You can use a tag or branch name 
instead of a commit hash to checkout a specific commit. If we checkout a tag 
or a commit hash, the **HEAD** will detach from a branch label when we commit, 
and no labels (apart from the HEAD) will move.

In the example above, if main was currently checked out and we wanted to checkout 
version 1.0.0, we could use the command:

`git checkout v1.0.0`

---
## Branches
When we apply a branch label and checkout the branch, future commits 
will move this label with the commits. By default, we will have a **main** 
branch. We can create a branch at the current head with:

`git branch <branch_name>`

![Alt text](git%20branch%20(1).png)

If we can make new branches, we ultimately need to recombine these 
branches when would want to, for example, accept a new feature or 
apply a bug fix. There are two ways to recombine branches: **merge** 
and **rebase**.

---
## Merge
A merge combines commits and forms a new commit with the combined changes. 
This means the new commit will have *two parents*. ![Alt text](git%20merge.png)

To merge, checkout the branch you'd like to merge to, and then use the 
command:

`git merge <branch_name>`

In the case above, the commands would be:

```
git checkout main
git merge feature
```

### Benefits of a Merge:
- Full history of the repository is maintained (can see both parents).
- Merges work well when collaborating because they are often few conflicts to resolve.

### Disadvantages of a Merge:
- Repository can get ugly and confusing with crossing parent lines as different commits are merged.

---
## Rebase
A rebase will 'copy' commits into another branch. This is like a 
transplant. 

![Alt text](git%20rebase.png) 

To rebase a branch onto another branch, checkout the destination branch and then 
run the command:

`git rebase <branch_name>`

In the case above, the commands would be:

 ```
 git checkout main 
 git rebase feature
 ```

### Benefits of a Rebase:
- Can keep the repository cleaner (changes are cleanly inserted without ties to parents).
- Rebases work well when working with personal local edits because you can "clean up" personal mess before sharing commits

### Disadvantages of a Rebase:
- Repository history/topology isn't maintained.

***Warning!*** **Do not** rebase commits that exist outside your local repository that people may have based work on.

---

## Commit Messages
Everything we have mentioned so far references commits extensively, so 
what is a needed for a good commit message?

Every time we commit, we should provide a message about the commit. When 
writing messages, there are a few standard idioms that you should follow.
Generally, a commit message should describe the problem being fixed or 
the feature being added in the commit, as well as why the change is 
being made. The message should be able to stand on its own (no links 
to other places) and shouldn't assume access to outside resources.

Structure wise, one can think of a commit message being similar to a 
letter. The first line of a commit message should be the subject of 
the commit. Subsequent lines are the message body and should include 
the what, why, etc., as well as list any known limitation to do with 
the commit. Text for commits should be wrapped at 72-80 characters.

The Golden Rule for Commits: the commit message must contain all info 
required to fully understand and review the patch/changes for correctness.

### The Do's and Don'ts of Commits:

When commiting...

### don't...
- mix whitespace/formatting changes with functional code changes
- mix unrelated functional changes
- submit all code as a single commit

### do...
- try to keep commits small and modular

Small commits makes it easier to review, revert, "blame", and troubleshoot!

---
## Git Commands

`git checkout <commit_hash>` opens up the version of the repository when 
the commit was made.

`git branch <branch_name>` creates a new label that attaches to future commits 
made from this label.

`git tag <tag_name>` creates a new label that attaches to a specific commit perminatly.

`git merge <branch_name>` combines commits and forms a new commit with the 
combined changes from the specified branch and the currently checked out branch.

`git rebase <branch_name>`copies commits into from the specified branch to the 
currently checked out branch.

`git log` shows the commit history below where you are checked out.

`git status` shows modifications made.

`git add <file_name>` adds a file in your working directory to the staging area.

`git commit` creates a snapshot of your repository with that can be addressed using 
its hash.

`git push` uploads staged local repository content to a remote repository.

`git fetch` downloads all the commits that the remote has that are missing from local.

`git pull` does a git fetch and merge.

`git restore --stadged <file_name>` removes staged files from staging area back to 
working directory.

---

![Alt text](meme.jpg)