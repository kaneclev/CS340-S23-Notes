# Lecture 21 outline, 4/5/2023

## Overview

In class we discussed localization of faults and the incorporation of the Ochiai and Tarantula formulas into the localized.py program. We started the topic of how to find which commit a bug occurred. We also started to download ruby. 

## Class Notes
Automate localization of Faults
- loaded a unit test suite from file
- ran with coverage

What data did we store:

    Lines covered on passing test

    Lines covered onf aling tests

    Total tests failed

    Total tests passed

Tarantula: $S(l) = \frac{\frac{failed(l)}{totalFailed}}{\frac{failed(l)}{totalFailed} + \frac{passed(l)}{totalPassed}}$

- tarantula function in LinuxLab
- tarantula scores (functional programs)

Ochiai: $S(l) = \frac{failed(l)}{\sqrt{totalFailed*(failed(l)+passed(l))}}$

### Debugging as Hypothesis Testing
Review Q: What makes up a good bug report?

Steps to reproduce $\rightarrow$ minimized (also apply to input data)

- Mozilla Engineers had lots of open bug reports that were not minimized
- Mozilla ran a Bug-a-thon crowd sourced simplification

Ex/ FF $\rightarrow$ print page causes a crash
- What part of the HTML is causing the crash?

Another problem where minimization can help:
- Yesterday your code worked, today it does not
- Why? - a number of commits
  - which commit?

>#### Definition
>**Causality** is influence by which one event, process, state or object (a cause) contributes to the production of another event, process, state or object, (an effect) where the cause is partly responsible for the effect and the effect is partly dependent on the cause
>#### Definition
>**Counterfactual** theories of causation:
>If A had not occurred, then C would not have occurred
- In software - the cause of a bug is precisely the difference between two versions

Can we find the commit that causes the failure?
- point that goes from work $\rightarrow$ fail

Idea: Replay commits $\rightarrow$ runtime? $O(n)$

Better way: Binary Search! $O(log(n))$

## Programs

```
# a simple implementation of a spectrum-based fault 
# localization using python coverage information
# need: test file, source file
import argparse
import coverage
import importlib
import unittest
import inspect
import os
import collections
import math 
# class to manage fault localization tallies
class FL:
    def __init__(self):
        # how many tests have passed and how many have failed
        self.totalpassed = 0
        self.totalfailed = 0
        # keep track of the lines that were executed on a failed test and a passing test
        # and how many times each was executed
        # a default dictionary calls the lambds 
        self.failed_lines = collections.defaultdict(lambda:0)
        self.passed_lines = collections.defaultdict(lambda:0)
    def passed(self, executable, missed):
        self.totalpassed += 1
        self._add_to_dict(self.passed_lines, executable, missed)
    def failed(self, executable, missed):
        self.totalfailed += 1
        self._add_to_dict(self.failed_lines, executable, missed)  
    def tarantula(self, line):
        """
        Calculate the tarantula (fault localization) score for a given line
        """
        if self.totalfailed == 0 or self.totalpassed == 0:
            return None
        numerator = self.failed_lines[line]/self.totalfailed
        denom = self.failed_lines[line] / self.totalfailed + self.passed_lines[line]/self.totalpassed
        if denom == 0:
            return None
        return numerator / denom
    
    def ochiai(self, line):
        numerator = self.failed_lines[line]
        denom = math.sqrt(self.totalfailed*(self.failed_lines[line]+self.passed_lines[line]))    
        if denom == 0:
            return None
        return numerator/denom
    def _add_line_to_dict(self, mapping, line):
        if line not in mapping:
            mapping[line] = 0
        mapping[line] += 1
    def _add_to_dict(self, mapping, executable, missed):
        # tested lines are the differecne between executable and the missed lines
        tested = set(executable).difference(set(missed))
        for l in tested:
            self._add_line_to_dict(mapping, l)
# create a command line argument parser object
parser = argparse.ArgumentParser()
parser.add_argument("test_file", help="path to the test file to run")
parser.add_argument("target_file", help="the file to localize")
# parse the command line arguments
args = parser.parse_args()
print(f"the test file is {args.test_file} and the target file is {args.target_file}")
# we need to import the test file as a module
module = os.path.splitext(os.path.basename(args.test_file))[0]
print(f"The module name is {module}")
spec = importlib.util.spec_from_file_location(module, args.test_file)
i = importlib.util.module_from_spec(spec)
spec.loader.exec_module(i)
print("Test module loaded...")
cov = coverage.Coverage()
fl = FL()
# use the inspect module to determine what is avaibile to us in a nother module
for name, obj in inspect.getmembers(i):
    if not inspect.isclass(obj):
        continue
    # load each test with unittest
    suite = unittest.defaultTestLoader.loadTestsFromTestCase(obj)
    # loop through the tests in this suite
    for test in suite:
        # first erase any coverage information
        cov.erase()
        # starting collecting coverage
        cov.start()
        # run a test and get its results
        res = test.run()
        #stop collecting coverage
        cov.stop()
        _, stmts, missing, _ = cov.analysis(args.target_file)
        if res.wasSuccessful:
            fl.passed(stmts, missing)
        else:
            fl.failed(stmts, missing)
print(f"We passed {fl.totalpassed} and we failed {fl.totalfailed}")
# need to calculate a tarantula score for each line in the code
_, stmts, _, _ = cov.analysis(args.target_file)
# map each line number to its tarantula score
# list comprehension (functional porgramming)
tarantula_scores = [
    (i, fl.tarantula(i)) for i in stmts if fl.tarantula(i) is not None
]
ochiai_scores = [
    (i, fl.ochiai(i)) for i in stmts if fl.ochiai(i) is not None
]
tarantula_scores.sort(reverse=True, key= lambda x: x[1])
ochiai_scores.sort(reverse=True, key = lambda x:x[1])
print(tarantula_scores[:30])
print(ochiai_scores[:30])
```

## Supplementary Material

Below is the txt file from Kevin's Website on how to download an updated Ruby and helpful git commands
```
We need an older version of Ruby to run this example. We can install it 
using `rbenv`, which is similar to Python's virtual environments.
Set up the environment:
  * sudo apt update
  * sudo apt install git curl autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm6 libgdbm-dev libdb-dev
  * curl -fsSL https://github.com/rbenv/rbenv-installer/raw/HEAD/bin/rbenv-installer | bash
  * echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
  * echo 'eval "$(rbenv init -)"' >> ~/.bashrc
  * source ~/.bashrc
  * rbenv install 2.7.8
  * rbenv global 2.7.8
github_url: https://github.com/floere/phony
good_tag: v1.9.0
bad_tag: v2.10.0
test_command: ruby -e 'require "./lib/phony"; Phony.normalize("999")'
We will use `git bisect` to find the commit where the failure begins.
Useful commands:
git bisect start: start a bisecting search
git bisect good: mark a commit as "good"
git bisect bad: mark a commit as "bad"
git bisect reset: get out of a bisecting search
git bisect run: run a script to automate the search (needs a good and bad mark)
```
## Something Fun

Loooking for bad apples!!
![image](https://user-images.githubusercontent.com/123112308/234955344-98d69c0f-4e19-49dc-b96b-343d0c25156f.png)
