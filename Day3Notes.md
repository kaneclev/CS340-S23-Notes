# Lecture 3 - 1/25/23

### Overview
This lecture focuses on defining new bash commands and scripting practices. Many useful bash commands are defined that we commonly used throughout the rest of the course.


### Basic Linux Commands:
#### Definition
**curl** - capture url
#### Definition
**pwd** - display the name of the present working directory.
#### Definition
**cd** - change directory
#### Definition
**ls** - view contents
#### Definition
**mkdir** - make directory
#### Definition
**man** - manual command, display information regarding other commands
#### Definition
**ssh** - secure shell, connecting to remote servers
#### Definition
**less** - view text information regarding a file
#### Definition
**cp** - copy a file or directory
#### Definition
**mv** - move a file or directory
#### Definition
**rm** - remove a file or directory
#### Definition
**grep** - pattern-matching, prints the lines that match a specified pattern within each file
#### Definition
**|** - piping, used to “pipe” the output of one command or program as the input for another command or program
#### Definition
**wc** - word count of a specified file (FLAGS -> -l = line count)
#### Definition
**basename** - prints the base name (name with no leading or trailing path) of a specified file or directory
#### Definition
**dirname** - print the directory path to specified file or directory
#### Definition
**xargs** - build and execute command lines from standard input
#### Definition
**cut** - remove sections from each line of a file (FLAGS -> -d = delimiter, -f = field)
#### Definition
**sort** - sort lines of text files
#### Definition
**uniq** - only return unique elements (no repeats)


### For Loop Structure:
	for i in {start..end..step}
	do
		echo $i
	done

	Variables: start - starting index of for loop, end - ending index of for loop, step - amount
  by which to iterate the current index at each step.


### Accessing Variable Values:
	To access the values of variables in our commands, we use the dollar sign character, $,
	followed by the name of our variable.
	
	Ex) for f in find random
	      do
		echo $f
	      done

	The above command echos the name of each file in the random directory to standard
	output.


### Connecting to your Linux Lab Machine:
	You will be assigned a local machine at the beginning of the year, and must enter your 
  information according to the below format and enter your password when prompted.

Format:
  YOUR_USERNAME@stlawu.edu@cslinuxlab-YOUR_NUMBER.stlawu.local


### One-Line Command Format:
	Commands such as the for loop illustrated above can be executed in one line when 
  utilizing the semicolon character. For example, the following for loops are equivalent:

for f in random
   do
	echo $f
   done

for f in random; do echo $f; done


### Manipulating and Accessing files in pwd:
  You can view the contents of your pwd with the ls command, and you can copy, move or remove any file or directory in the pwd with the 
  commands cp, mv, and rm respectfully. You can also back out a level from your current directory with the command cd .., as well as 
  move to other subdirectories via cd DIR_NAME.


### For Loop File Globbing:
for i in random/*
	do
	echo $i
	done

The above for loop includes an asterisk following the random/ directory. This technique is referred to as file globbing, 
in which the use of a wildcard character such as an asterisk gets expanded upon execution of the command to relevant 
files and directories.


### Using Man for Command Instruction
	The man command is useful for finding information regarding any of the linux 
  commands. This command provides you with the name of the command, formatting,
  uses, and much more helpful information.


### Pattern-Matching with grep
  The pattern matching command grep can be utilized in combination with escape characters to match file names or contents 
  based on the rules specified by the escape characters. For example, including a carat (^) at the beginning of the string 
  following grep will ensure that we pattern match files whose names begin with the specified string. Similarly, we can 
  use the dollar-sign ($) at the end of the string following grep to ensure that we only pattern match with files whose 
  names end with the specified string. Using these in combination enforces both of the rules, which is to say that the result 
  of the pattern-matching will only contain files that both begin and end with the specified string. Finally, we can utilize 
  two escape characters (\\) to specify when we’re using other special characters such as wildcards and dots as information 
  within the string rather than separate commands.

Ex) find random | grep ^\\.ac$; output -> files that begin and end with the string “.ac”.


### Command Substitution
	Using the same method by which we accessed our values of previously defined 
  variables, we can also run a command and provide it’s output as text in the command 
  line arguments for another command.

Ex) for i in {0..#(find random | grep ace | wc -l)}
	do
	  echo $i
	done


#### Definition
**xargs**
  The xargs command builds and executes command lines from standard input.

Ex) xargs basename | grep ^9; 
  Output -> using standard input as params to xargs, print the basename of all files of the xargs specified name and 
  pattern-match the result for names beginning with the character 9.


### Conditional Statement Structure
	Conditionals work by ending the statement with if in reverse (fi).
Ex) if [ -f $f ]; then do echo $f; fi;


### Exit Code
You can view the exit status of a program’s execution using echo $?
#### $? - Exit code of previously executed program, 0 upon success and failure otherwise.


### Redirecting Output (Standard and Error)
	You can redirect output from a program into a file of your choosing using the greater than symbol.
Ex) find random > randomfiles.txt

