# Lecture Notes: Day 22
## Date: 04/10/2023

## Git Bisect
Git Bisect is a tool that allows us to find the commit that introduced a bug in a project by performing a binary search through the commit history. This process involves identifying a known bad commit and a known good commit, and then checking out a middle commit between them to test if the bug is present or not. Based on the result, we can then eliminate half of the remaining commits and repeat the process until we find the faulty commit.

## Using Bisect
To use Git Bisect, we first need to identify a known good commit and a known bad commit. First, to do an exercise on Bisect we need to set up the enviroment. To run Git Bisect, we need a program that run the language Ruby. Because the version of Ruby we need is not the one we can install by default on our Linux lab machine, there are steps we need to do to set up the environment.

## Steps to set up Ruby environment:

```
sudo apt update
sudo apt install git curl autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm6 libgdbm-dev libdb-dev
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/HEAD/bin/rbenv-installer | bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
rbenv install 2.7.8
rbenv global 2.7.8'
```

When using bisect, we need the last commit where the code worked and the first commit where the bug appeared. Once we have these, we can use the following command to start the bisect process:

To start a bisecting search
`git bisect start`

After running this command, Git Bisect will checkout a middle commit between the bad and good commits and ask us to test if the bug is present or not. We can use the following commands to mark the current commit as good or bad, respectively

To mark a commit as "good"
`git bisect good`

To mark a commit as "bad"
`git bisect bad`  

Based on our response, Git Bisect will then checkout another commit for us to test, and the process will continue until the faulty commit is identified

## Manually using Git Bisect
Identify a "good" commit where the issue doesn't exist and a "bad" commit where the issue exists.

`git bisect start`

Mark the "good" commit with 
`git bisect good <commit>`

Mark the "bad" commit with 
`git bisect bad <commit>`

Git will automatically checkout a new commit and prompt to test whether it's "good" or "bad".
Continue marking "good" or "bad" until the first commit that has the issue is identified.
Run git bisect reset to exit the search.

## Automatically using Git Bisect
Git Bisect can also be automated by using a script to perform the testing and marking of commits. This is useful when the testing process is time-consuming or requires human intervention. To automate Git Bisect, we need to write a script that returns a zero exit status if the bug is not present and a non-zero exit status if the bug is present. We can then use the following command to start the bisect process

Run `git bisect start`

Mark the "good" commit with 
`git bisect good <commit>`

Mark the "bad" commit with 
`git bisect bad <commit>`

To automate the search
`git bisect run <script>`

Example:
```
git bisect start
git bisect good
git bisect bad   
git bisect run <script>
``` 
* Exit 0 “good”
* Exit 1 “bad”

Git Bisect will then use the script to test and mark the commits until the faulty commit is identified

## Phony 
The Job of Phony is to take a phone number that is typed in and turn it correct formatted output 
Phony works with international numbers only such as 61 412 345 678!
The goal of this phony is to be able to normalize/ format/ split all phone numbers in the world
Using phony on our Linux machine.

First, we need to checkout the version of phony that will work for the example we are doing, and we will use its tag. The point of tag in a repository is used as a permanent name for the one of the commits. Like a version of phony:

`git checkout v1.9.0`

Format command in phony will take a string of different phone numbers and change it to a correct format of phone number:

`ruby -e “require “./lib/phony”; puts Phony.format(“13152291875”);’` ------------------------ +1 315 229 1875

The normalize command will take a string of phone number and change it back to strings of numbers:

`ruby -e “require “./lib/phony”; puts Phony.normalize(“+1(315) 229-1875”);’` ----------------- 13152291875

## Example using normalize:
```
git checkout v2.10.0
ruby -e “require “./lib/phony”; puts Phony.normalize(“999”);’ 
```

This broke the program, meaning some where between the commit tag v1.9.0 and the commit tag v2.10.0 , we have a commit that broke this functionality for normalize(“999”).We want to know where along the way this broke or stopped working and to do that, we can do a binary search.

Git allows us to automate that binary search and this tool in git that will do the binary search is called bisect.

## Actual cause
When we have a problem with our code, we need to find the cause so we can fix it. One way to do this is by using a tool called git bisect, which helps us identify the commit that introduced the problem. The parts of the code that changed between the good and bad versions are what we call the "actual cause" of the problem.

To fix the problem, we want to make as few changes as possible to the code. This means we want to have a lot of overlap between the good and bad versions of the code, and we want the "actual cause" to be the minimal amount of change needed to fix the problem.

![An Actual cause](https://drive.google.com/uc?id=13j_B7F1iZCOQkRF6anG6-YkUsofJP8K5)


However, finding the minimal set of changes that caused the problem can be a challenging task. To simplify things, we make an assumption that if removing any changes from the set would make it "not interesting," then we have found a one-minimal set. This is a way to further minimize the changes needed to fix the problem

## Minimizing Test Cases
When dealing with a large number of test cases, it can be time-consuming to test each case individually using Git Bisect. In this case, we can use minimization techniques to identify a minimal set of test cases that reproduce the bug. One technique is to use a tool like Delta Debugging, which iteratively removes parts of a failing test case until the minimal set of parts that still reproduce the bug is found.

In conclusion, Git Bisect is a powerful tool for identifying the commit that introduced a bug in a project. By using a binary search through the commit history, we can quickly identify the faulty commit and fix the bug. Additionally, by automating the process and minimizing test cases, we can save time and effort in the bug-fixing process.
