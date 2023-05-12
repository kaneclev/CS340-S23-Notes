# ***Day 8 Outline - 2/13/23***

## **Overview**
This lecture begins with a warmup and quick review of commit ettiquette. We continue on with learning about git repos and syncing changes. Next is the workflow for git repos and the beginning of quality assurance.

### **Today's warmup**
- 2 branches
- 3 commits to main
- 4 commits to feature
- rebase feature onto main

---

### **Review - good ettiquette for commits**
1. Commit message should describe contents of changes
2. Seperate out functionality/formatting changes
3. Smaller commits
4. Don't assume outside resource access (Links to external sites)
5. wrap messages for ease of reading (72-80 characters)

>#### ***Overall goal is team efficiency***
>-> easier review  
>-> easier to troubleshoot  
>-> easier to revert  

---

### **Collaborating with Git Repos**
- Connect a repository to another copy of the repo by specifying a remote

Git is a distributed version control system. 
Each Developer has own copy of the commit tree. 
You must sync these changes with the other copies of the repo.

git remote -v --> list remote repositories

---

### **Syncing Changes**
Git fetch   
- downloads new commits from the remote  

Git push  
- uploads our new commits to the remote  

Git fetch && git merge origin/...
- git pull -> fetches and merges    

Git merge origin/main

>Note: all remote branches prefixed with remote name  
>- EX. origin/main

>Once you push to a remote, assume you cannot change those commits
>- Someone might use one of the commits as the basis of their work

---

#### **General Rule of thumb**
- Rebase unshared changes
- Merge with shared changes

---

### **Permissions on Remote repo**
Principle of Least Priviledge
- For "reasons", you typically only have write permissions 
to your own repos on a site like Github

We won't be able to push  
- can't sync our own changes

---

### **Challenge:** 
#### **How do we commit to a repo that does not grant us write permission**
> **Definition**
>
>**Pull Request**: Request for a developer to pull your commits into their upstream-repo

![image](Day_8_flowchart.png)

---

### **Typical Workflow to contribute to a git repo:**
1. Assign self issue/bug report
2. Fork repo/clone
3. Make a branch for bug fix
4. ***Commit to new branch***
5. Push to our fork
6. Open our pull request (PR)
> Note: Any additional commits on this fork branch get added to PR

---

### **Quality Assurance and Testing**
Want to deliver high-quality software at low cost  
How do we increase, asses, and assure software quality?

> **Definition**
>
>**Quality Assurance**: is the maintenance of a desired level of 
>quality in a service or product, especially by means 
>of attention to every step of the process of 
>delivery or production.

![Alt Text](https://ih1.redbubble.net/image.679500044.5211/st,small,507x507-pad,600x600,f8f8f8.u4.jpg)
