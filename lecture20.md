# Notes Lecture 20
# 4/3/2023

## Overview
In class 20 we started with a short summary of class 19. Then we talked about different techniques of fault localization. We touched on the problem of scale with big code bases and talked about spectrum based fault localization as a possible solution for this. For the rest of the class we wrote a program: localize.py to implement spectrum based fault localization. 

## Quick Summary of class 19: 
- fault localization - implicating lines of code in a bug/fault/defect
- techniques:
    - add print statements -> detect where code is reaching, risk of
      flushing output buffers
    - using debugger

## Code Tracing
- Problem of scale in big code bases

Instead, write script that can help with this
Automatically filter using coverage to minimize lines of code to analyze
Bug will be in covered lines
 - deprioritize passing test coverage
 - prioritize failing test coverage

 ## Class 20:
 Example of writing a tool that can help us with automitcally filter bugs.
 Wrote Python script that can run unittest and calculate coverage 
 and weight. 

Looked at a commit we knew had a bug but all tests were passing
    - verified defect by creating test that will expose bug
    - Checked out test file from commit that fixed the bug
    - ran unittest again, failed!
    - Looked at stacktrace, had a format error.

 We will write localize.py which can run on any python program
 and unitest.
  - GOAL: Localize which line the bug is on using our program

 Handling command lines using argparse, similar to GetOpt in Java

This mostly includes what was written in class 20
(further progress was made in class 21)

 Localize.py:

```
# a simple implementation of spectrum-based fault localization
# using python coverage information
# imports

import argparse
import collections
import importlib
import inspect
import math
import os
import unittest

import coverage

# adding FL class with methods
# class to manage faults localization tallieds
class FL:
    def __init__(self):
        
        # how many tests have passed and how many have failed
        self.totalpassed = 0
        self.totalfailed = 0

        # keep track of lines that were executed on a failed test and a passing test
        # and how many times each was executed
        # create a dictionary, if key not found, lamda returns default value of o
        # defualt dictionary calls the lamda function if key is not found
        # the lamda returns the default value
        self.failed_lines = collections.defaultdict(lambda: 0)
        self.passed_lines = collections.defaultdict(lambda: 0)

    # add passed
    def passed(self, executable, missed):
        self.totalpassed += 1
        self._add_to_dict(self.passed_lines, executable, missed)
    # add failed
    def failed(self, executable, missed):
        self.totalfailed += 1
        self._add_to_dict(self.failed_lines, executable, missed)

    def _add_line_to_dict(self, mapping, line):
        if line not in mapping:
            mapping[line] = 0
        mapping[line] += 1

    def _add_to_dict(self, mapping, exacutable, missed):
        # tested lines are the difference between the executable lines and the missing lines
        tested = set(exacutable).difference(set(missed))
        for l in tested:
            self._add_line_to_dict(mapping, l)    


# Command line handling
# create a command line argument parser object
parser = argparse.ArgumentParser()
parser.add_argument("test_file", help="path to the test file to run")
parser.add_argument("target_file", help="the file to localize")

# parse the command line arguments
args = parser.parse_args()

print(f"The test file is {args.test_file} and the target file is {args.target_file}")

# we need to import the test file as a module
module = os.path.splitext(os.path.basename(args.test_file))[0]
print(f"The module name is {module}")

spec = importlib.util.spec_from_file_location(module, args.test_file)
i = importlib.util.module_from_spec(spec)
spec.loader.exec_module(i)

print("Test module loaded...")

# create coverage objcect
cov = coverage.Coverage()

# Create fault localization object
fl = FL()


# use the inspect module to determine what is available to us in another module
for name, obj in inspect.getmembers(i):
    # skip over non-class members
    if not inspect.isclass(obj):
        continue

    # load each test with unittest
    suite = unittest.defaultTestLoader.loadTestsFromTestCase(obj)

    # loop through the tests in this suite
    for test in suite:

        # first erase any coverage information
        cov.erase()

        # start collecting coverage
        cov.start()

        # run a test and get its results
        res = test.run()

        # stop collecting coverage
        cov.stop()

        # create variables for use in FL class later
        _, stmts, missing, _ = cov.analysis(args.target_file)

         if res.wasSuccessful():
            # adding passed test
            fl.passed(stmts, missing)
        else:
            # adding failed test
            fl.failed(stmts, missing)

# Printing passed and failed tests
# A way to control our implementation because we knew only
# 1 test was failing
print(f"We passed {fl.totalpassed} tests and failed {fl.totalfailed} tests")

````

## This is where we end class 20 

Localize.py does not yet have the ability to help us with that lines are
interesting. This will be covered in class 21 were we will use
tarantula and Ochia to help with weighting. 

## Key takeaway:
 - Spectrum based fault localization
 - Goal to rank lines where the bug/defect probably is
   to help us to fault localize more efficiently
 - Program not done yet




 

