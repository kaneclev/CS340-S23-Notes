# Style Guide

## Overview
This document is the style guide for the CS340 lecture notes. There are three sections to the style guide. The first and second sections give notes and code formatting guidelines. These guidelines generally follow the [Markdown Guide](https://www.markdownguide.org). The third section describes what should and should not be included. Essentially, everything that is written on the board and code examples should be included. 
____

## General and Notes Formatting
The format of class notes and study guides should follow the [Markdown Guide](https://www.markdownguide.org) format. Notes written on the board (these are the notes that Dr. Angstadt takes on his iPad) should follow the format which they were originally written in as much as possible. The notes tend to be a mix of lists, definitions and small chunks of text, so the notes in this repository should be lists, definitions and short chunks of text in paragraph style. Since these three things are used most often, a few comments are made about each of them. Overall, the formatting of the notes for this project should follow the [Markdown Guide](https://www.markdownguide.org). 

### Lists
The class notes often contain lists. Some lists are ordered and others are unordered. For this repository the notes should reflect what was put on the board in class, so if the list was ordered in class, it should be ordered here and vice versa. The same goes for indentation. If what was put on the board contained an indented list, the notes in this repository should reflect that.

### Definitions
Definitions show up quite frequently in the notes, and they tend to be some of the most important pieces of information. Because of this, whenever there is a definition, it should be treated as a block quote. The first line of the quote should be denoted by a heading which says "Definition". This heading should not be a major heading. Level four is appropriate for this. The term being defined should be in bold. An example of formatting for definitions is the following.

>#### Definition
>This is an **example** of how a definition should be formatted.

### Chunks of Text
Chunks of text should be formatted as paragraphs.

### General Formatting: Sections
Each major section should have an appropriate heading. Major sections should be separated by horizontal rules. Major sections should generally be major topics which are discussed in class, but the exact definition is largely left open to the interpretation of the author. Examples of major sections in this style guide are *Overview, General and Notes Formatting, Code Formatting,* and *What to Include*.

Sections that are not major sections should be denoted by headings but should not be separated by horizontal rules. Examples of sections that are not major sections are *Lists, Definitions,* and *Chunks of Text*.

### General Formatting: Naming Conventions
Files containing class notes should be named in the following way: *DayXNotes.md*. X should be replaced with the lecture day of the notes, so for day nine, the notes should be named *Day9Notes.md*. 

The study guides should be named *Exam1StudyGuide.md* and *Exam2StudyGuide.md* respectively. The course overview should be named *CourseOverview.md* and the style guide should be named *StyleGuide.md*. 
_____

## Code Formatting
Like the notes, the code format should follow the [Markdown Guide](https://www.markdownguide.org). 

### Programs From Class
Any code written in class that is a line of code or greater should be formatted as code blocks. This includes all major programs we have written. An example of this can be seen below.

```
Blocks
of
code
should
be
formatted
like
this.
```

### Specific Commands and Git and Bash Commands
Specific commands mentioned alone should be formatted as code in line with the text, not as blocks. In the [Markdown Guide](https://www.markdownguide.org/basic-syntax/#code), this is denoting a word or phrase as code.

Git and Bash commands should be on their own line with a brief description of what they do. They should be formatted in the same way as specific commands. This means that the bash command itself should be treated as a word or phrase which is being denoted as code. Git and Bash commands can be in list or paragraph format, but should be on their own line. An example of how a Git or Bash command should be formatted can be seen below.

`cd` change directory

If several Bash commands appear in a day of lecture notes, it is recommended that they be included in their own section titled *Bash Commands*. The same goes for Git commands appearing in a section titled *Git Commands*.
____

## What to Include

### Overview
A brief overview should be included at the beginning of the notes. This should include each of the major topics covered and a scentence or two giving a brief description or overview of the topic.

### Class Notes
As a general rule of thumb, anything that is written on the board during class should be included in the notes. Exceptions to this are things like updates on deadlines that are only relevant at the time of the lecture and are not part of the course material. Other than things like that, everything that is written on the board should be included. 

### Programs
All programs and code written in class should be included. Programs should include all comments included by Dr. Angstadt. Other comments which help to clarify what the code is doing are encouraged. On a few occaisons, quick examples were run through as a brief tangent. It is up to the author on whether to include these or not.

### Git and Bash Commands
The rule of thumb for Git and Bash commands is if in doubt include it. All new and rarely used commands should be included in the notes along with a brief description of what the command does. The description does not need to rewrite the manual page for the command, but a reader should be able to gain an idea of what it does based on the description. Whether a command is commonly or rarely used is left up to the author, but the author should include the command if they are unsure if they should include it or not. 

### Websites and Supplementary Material
If websites are used during an exercise or example in lecture, a link should be included in the notes. If photos, diagrams, or other visual aids are used during lecture, they should also be included. In the case of diagrams, photos of hand drawn diagrams are acceptable, but the author should do their best to make them as neat and ledgible as possible.

### Warmups
If a lecture began with a warmup or exercise, a brief description of the exercise should be included. This should include what the problem itself and a brief description of the solution. Depending on the exercise, a solution should also be given. For example, if the exercise was to write a script that accomplishes a specific task, the script should be included.

### Group Presentations
On several occaisons we have created slides as small groups. These slides do not need to be included in the notes, however a description of the material covered by each of the slides should be included. 

### Industry Guests
In the notes for days when an industry guest visited, a description of the visit should be included. The description should include a brief biography (who they are, where they work, what their role is) and a description of some of the highlights of the conversation. The highlights should include the question they were asked and the main points the guest made in their answer. 

### What Not To Include
Please refrain from including personal comments and opinions on the material. Clarifying comments and useful ways of thinking about concepts are encouraged in the notes, but personal comments and opinions on things like how much you like the topic should not be included. 

### Something Fun
This is optional, but everyone is encouraged to end their notes with something fun. This might be an image, meme or anything that will make us laugh.