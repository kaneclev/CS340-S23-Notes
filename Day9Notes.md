# Lecture 9 Notes
# 2/15/2023


### Overview
Lecture 9 covered began the coverage of Quality Assurance (QA), along with examining the more specific variations of quality: External and Internal. We also covered Rice's Theorem, in which we understand that no program can ever tell us if a software is correct. Finally, we ended off on potential alternatives to using another progrem to determine correctness of our Software.

### Warmup Exercise
*Lecture starts with a warmup*
Warm-up: Set up your linux machine to support ssh with github
    - Look up documentation for public/private key
    - Fork github.com/kevinangstadt/CS340-S23-Notes
    - Checkout Day9 Branch
    - Submit a pull request (PR) updating the table with the number of files in your home directory
        - Follow good commit practices

</br>

### Quality Assurance:
    - Who consumes a piece of software?
        - The end user or customer
        - The Developer

    - There are two types of quality:
        1) **External Quality**: Customer facing; Easy to use; The performance; Should do or output the right thing
        2) **Internal Quality**: Developer facing; Source code should be readable, well documeneted and easily maintainable

    - If the dominant activity of software engineering is maintainence, then internet quality is mostly a measure of maintainability

    - How do we ensure and assure maintainability?
        - Human code review
        - Code anlysis tools and "linters"
            - **Linter**: A simple checker that checks some property within the code
            - **Code Analysis Tool**: More indepth by parsing the code and analyzing the code itself.
                - An example of this is a type checker
        - Use programming idioms and design patterns
            - Defining classes or objects using predsigned pattern is an example of a design pattern
        - Follow local coding standards
            - A company style guide would be an example of a local coding standard
</br>

### External Quality
    - **External Quality**: What does doing the right thing mean?
        - Doing the right thing means that the software behaves according to the specification (what makes a good spec)
        - Doesn't do the "Bad thing"
        - Possible bad things:
            - Crashes
            - Causes death
            - Wrong outputs
            - Security breaches or leaks

    - How do we handle the inevitable failure?
    - Robustness against maintence mistakes
        - Do fixed bugs sneak back into the code?

</br>

### Rice's Theorem
    - Why don't we just write a new program X to tell us if our software Y is correct?
        - **Rice's Theorem**: Presents X from always giving the right answer
            - All non-trivial semantic properties are undecidable
    
    - Note: X is not always wrong, but X is not always right either and we don't have a way of knowing the difference

    - What should we do instead?
        - We approximate and use heuristics
        - Use things like type checkers, linters and static analyzers

</br>