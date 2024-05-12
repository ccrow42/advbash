### Introduction

Processes text for rows and columns


awk is its own programing language, so it doesn't follow conventions.

awk 'code block' file_to_process

`awk 'NR == "2" { print $3 }' text.txt`

NR stores the number of lines contained in the text file

The above will print the second line and third column of the file

awk is a domain-specific language - designed to address the needs of a specific subject area


### awk -print

awk '{}' # action block

single quotes are not part of the block, it just prevents variable substitution. Awk is a language and has its own variables.

awk can print a literal such as:
`awk '{print "hello", "world"}' < abc.txt`

the above will print "hello world" for each line in the abc.txt file

$1 $2 $3 are positional values to represent columns


### awk build-in variables

NR number of records
NF number of fields
FILENAME the filename that was passed, is null if using STDIN
```
df -h > size.txt

awk '{ print NR, $1, $4 }' size.txt

# we can use conditions

awk NR == 4 '{ $1, $4 }' size.txt # only returns the 4th line

awk '{ print NF }' size.txt

awk '{ print "Number of columns in line: " NR, "is " NF }' size.txt

print '{ $NF }' size.txt

awk '{ print FILENAME }' size.txt # will be null if there was not a filename

```

### awk Option -F

-F specify the field separator

`awk -F ":" '{ print $1 }' sizeV1.txt`


### awk Option -v

-v used to declare a variable before executing the action block or program

`awk -v var="Hello, World!" 'BEGIN { print var }'`
BEGIN keyword tells awk to execute the action block before text processing, which in effect bypasses it.

BEGIN is part of the PROG block, instead of the ACTION block

`awk -F "|" -v high_sarary="90000" '$7 >= high_salary { print $2 }' employees.txt`

`awk -F "|" -v high_salary="90000" -v low_salary="65000" '$7 >= high_salary || $7 <= low_salary { print $2 }' employees.txt`

variables quickly identify the intention of the program

### awk Programs From Files

``` hello.awk
#!/usr/bin/env awk -f

BEGIN {
    hello = "Hello"
    FS = "|"
    print hello, "world!"
}

{
    print $2
}
```

```
#!/usr/bin/env bash
awk -F "|" -v hello="Hello" 'BEGIN {
    print "Hello, World!"
}'
```

### awk Bash-Hybrid

```
#!/usr/bin/env bash

readonly UP_HEADER="=====Needs to be adjusted up====="
readonly DOWN_HEADER="=====Needs to be adjusted down====="

high_salary="${1:-90000}"
low_saraly="${2:-65000}"


awk -F "|" -v high_sarary="${high_salary}" -v low_salary="${low_salary}" -v up_header="${UP_HEADER}" -v down_header="${DOWN_HEADER}" '
$7 >= high_salary {
    if (!printed_down_header) {
        print down_header
        printed_down_header = 1
    }
    print $2, $3, $7
}
$7 <= low_salary {
    if (!printed_upHeader) {
        print up_header
        printed_up_header = 1
    }
    print $2, $3, $7
}'
```

```



