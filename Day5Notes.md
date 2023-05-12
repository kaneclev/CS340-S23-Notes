# Lecture 5: Shell Scripting
##

### Overview
This lecture focused heavily on practicing BASH scripting skills in order to complete a tangible task; handling COVID data.  

### **Scripting 'covid.sh':**  
In the last lecture, we worked on a shell script called 'covid.sh'.  
The purpose of our 'covid.sh' script is to collect COVID data from the New York Times,  
and represent it using our shell.

The following code is what we have so far:  
```  
#!/bin/bash

# make a temp file to store the covid data
temp_file=$(mktemp)

# download the latest NYT covid data and store it to our temp file
curl -s -k -o $temp_file https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv

# print the covid data to the shell
less $temp_file 

#clean up the temporary file
rm $temp_file
```


**Using Command Line Arguments in BASH**  
Arguments come after the executable and are an array of strings.  
We refer to these arguments with indices $1, $2, ...$n.  
To combine these arguments, we can add quotation marks to make two string arguments into one; i.e.:  
`- { "New York" }` instead of `{"New", "York"}`

**Checking for Bad Arguments**  
We can use if statements in BASH to filter out bad arguments.  
To do this, we use an if statement with a *-z* flag to make sure an argument exists.  
```
if [ -z "$state" ]
then
    echo "Usage: $0 state"
    rm $temp_file
    exit 1
fi
```

**Parsing a File**  
We want to be able to grab what we want specifically from our data, without  
including unnecessary columns or lines.
- *head* allows us to grab the top of the file.
- *tail* allows us to grab the end of the file.  

Using these flags, piping, and a delimiter, we can not only cut out   
unnecessary pieces of the header like the state name and the 'fips' column,  
but we can also create an if-statement to validate that the state is in our data.  
```
# check to make sure the state exists within our file 
# first cut out unecessary parts of the file and then search for our state
state_check=$(tail +2 $temp_file | cut -d ',' -f 2 $temp_file | grep "$state")
if [ -z "$state_check" ] # if no such state exists
then   
    echo "No data for $state"
    rm $temp_file
    exit 2
fi

# output the header and cut out new york & 'fip' because it isnt necessary
head -n 1 $temp_file | cut -d , -f 1,4-5 
```

**Modifying How We Represent the Data**  
Currently, our script can output COVID data representing the total cases/deaths cumulatively for each day,  
but we can modify it to instead represent daily change using a *for-loop* and some math.  

We can use double parentheses to perform math operations, like (($variable)), or ((number)).  

```
# for each entry in our file, specifying which state and which columns we want, let's loop
for entry in $(grep -i "$state" "$temp_file" | cut -d ',' -f 1,4-5)
do
    # entry is a single line for the data
    # assign a var for each piece of each entry we want
    date=$(echo $entry | cut -d ',' -f 1)
    cases=$(echo $entry | cut -d ',' -f 2)
    deaths=$(echo $entry | cut -d ',' -f 3)
    
    # echo the date we are currently on 
    # subtract the previous deaths from the current deaths
    # subtract the previous cases from the current deaths
    # then, echo them in the proper formatting.
    echo $date,$((cases - prev_cases)),$((deaths - prev_deaths))

    prev_cases=$cases
    prev_deaths=$deaths

done
```
With each of these pieces outlined, we can put them together and our script will generate  
a comprehensive set of data.  

Below is the full 'covid.sh' script:


```
#!/bin/bash

# we need to download the latest NYT covid data and print out a report for a given state.
# make a temp file to store the covid data
temp_file=$(mktemp)



curl -s -k -o $temp_file https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv


# read state using command line arguments i.e.) ./covid.sh "New York"
# this assigns state to the first command line argument
state=$1

# check that command arg isnt empty
if [ -z "$state" ]
then
    echo "Usage: $0 state"
    rm $temp_file
    exit 1
fi

# check if the state is actually in our data
state_check=$(tail +2 $temp_file | cut -d ',' -f 2 $temp_file | grep "$state")
if [ -z "$state_check" ]
then   
    echo "No data for $state"
    rm $temp_file
    exit 2
fi




echo "Covid cases and deaths for $state"

# Output daily deaths

prev_cases=$((0)) # double parens indicates an integer/an expression
prev_deaths=$((0))


# output the header and cut out new york & 'fip' because it isnt necessary
head -n 1 $temp_file | cut -d , -f 1,4-5 


# grep state info from temp file

# exclude the header line so that we dont accept faulty greps 
for entry in $(grep -i "$state" "$temp_file" | cut -d ',' -f 1,4-5)
do
    # entry is a single line for the data
    date=$(echo $entry | cut -d ',' -f 1)
    cases=$(echo $entry | cut -d ',' -f 2)
    deaths=$(echo $entry | cut -d ',' -f 3)

    echo $date,$((cases - prev_cases)),$((deaths - prev_deaths))

    prev_cases=$cases
    prev_deaths=$deaths

done




# remove the temp file to avoid filling up space with useless stuff
rm $temp_file
```