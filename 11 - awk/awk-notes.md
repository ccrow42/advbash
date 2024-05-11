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

`awk -F ":" '{ print $1 }' sizeV1.txt

