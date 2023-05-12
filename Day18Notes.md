# Day 18 Notes

## Overview
This note document highlights the topics covered in class on 3/27/23. This will begin the lectures on Defect reporting and triaging. First we went over a bunch of definitions and then went through the steps a bug would follow (see day 19 notes for continuation).

---

## Defect Reporting and Triaging 
Mozzilla in 2005 reported 300 bugs a day that needed to be triaged.

#### Fualt
A **Fault** is an exceptional situation at runtime.

#### Defect
A **Defect** is any character of a product that hinders its usabiulity for intended purposes. 
                (ex. design defect or a bug (static defect))

#### Defect Report
A **Defect Report** provides info about fault or bug created by tester, user, tool containing lots of detail.

#### Feature Request
A **Feature Request** is a potential change to indended purpose of software.

An issue is the union of a defect report and feature request.

#### Defect Report Life Cycle
A **Defect Report Life Cycle** is made of possible stages & actions, including reporting confirmation, triage, assignment resolution and verification. 

See bug diagrams on course webstie from lecture 18.
There are many paths through life cycle and reports follow differant paths. Ie not a linear process
Status of a report tracks position in lifecycle

---
## Bug Life Cycle
### 1.) How does report enter system?
-    Internal - Developers Qaulity Assuarance, Testers
-    External - Beta-tester, end user, 

-    Anatomy of a bug report - 
     -    summarry/title 
     -   Description of bug/defect
     -  Component
     -   Version
     -   OS
     -   Steps to reproduce faults
     -   Attachments such as datafiles, screenshots, stacktraces, videos

### 2.) Triaging: Which bugs get fixed first?
-    Assignment of degrees of urgency 
-    Severity - degree of impact on developer or operation of component.
-    Priority - Importance or urgancy of fixing defect. 
-    Severity and priority are correlated but independant 
-    Triaging helps cost benefit analysis as more reports then resources
     -   How expensive is bug to fix?
     -   How expensive is bug to NOT fix?

---
