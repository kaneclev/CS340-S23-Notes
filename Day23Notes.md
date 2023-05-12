# Lecture 23 notes

## Overview
In this lecture, we learned about Delta Debugging which was used in 
Project 2. We also learned about one-minimal and local minimums.

## Delta Debugging - Glorified binary search
Given:
- a set C= {C1, C2... Cn} 
- a function Interesting: C -> {Yes, No}
- Interesting(C) = Yes
Interesting in monotonic, unanmbigous, and consistent

## Our Assumptions
1. Any subset of changes may be interesting (not just single changes)
2. Interesting is monotonic
    - Interesting(x) -> Interesting(x ∪ {c})
3. Interesting is unambiguous
    - [Interesting(x) AND Interesting(y)] -> Interesting(x ∩ y)
4. Interesting is consistent 
    - Interesting(x) = YES or Interesting(x) = no

Why can't <br /> 
Interesting (P1) = YES and Interesting (P2) = YES
because unanmbiguous Interesting(P1 ∩ P2) = {}

But!<br /> 
Interesting(P1) = NO and Interesting(P2) = YES because consistent: <br /> 

If this is the case, By monotone:
<br /> no subset if interesting, the interesting subset is a comnination of elements from P1 and P2



