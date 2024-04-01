# Scriptflow

## if statements


#### use double square because it allows a wider range
if [[ 3 > 4]];; then


#### will handle later
'''
case word in
  pattern1)
    statement
    ;;
  pattern2)
    statement
    ;;
'''

for, while and until loop.
'''
for i in {1..3}; do
  do something
  echo "$i"
done
'''

for is predefined, until variable condition
'''
for i in $(seq 1 3); do
  do something
done

seq 1 3 | while read i; do
    do something
done
'''
All loops have a do and a done keyword

for is better when we know how many interations

while is better at reading files

while and until when we don't know


#### source
. or source will execute the commands in a different file as if they were in the same script


Consider using an eval to ensure the script is there, for example:

readonly CONF_FILE=".conf"
if [[ -f ${CONF_FILE} ]]; then
  source "${CONF_FILE}"
else
  do something else
if

## functions

**git example**

```
#!/bin/bash
git_url=$(1)

clone_git() {
  git clone ${1}
}

find_files() {
  find . -type f | wc -l
}

clone_git "${git_url}"
find_files
```

There is a function keyword. It is also possible to use a one liner.

### local variables

```
you can use a local variable
my_function() {
  local var1="Hello"
}
```


### Lab 1

**Basename** - return non-directory portion of a pathname


### Arguments

The shift command shifts the arguments down one position


### pids

strace -Tfp <PID>
Timing + child + parent shell

kill -9
kill -15




### nohup

don't associate script with the current tty

### built-in commands

*built in commands are built in to the shell*

e.g. echo.

use the built in type command we can tell if a command is built-in

built-in commands do not create a new pid



### kewords vs builtins

***NOTE:*** To see all keywords, type compgen -k. To see all built-ins, type compgen -b

keywords control execuction structure

built-ins are just commands and also designed to be used in an interactive shell session

[] is for a built-in, it runs the test command (you can check with man test or man [)

[[]] is for keywords and is evaluated directly by the shell

the difference is in the range of evaluations that each can perform. Consider the example:

[ 1 < 2 ] && echo "1 is less than 2". This will error because < is a redirect symbol.

[[ 5 < 7 ]] works and is more modern


[[]] also supports the folowing:

- you can group expressions: [[ 3 -eq 3 && (2 -eq 2 && 1 -eq 1) ]]
- pattern matching: name=$"Bob Doe" [[ $name = *o* ]] && echo "patterns can be used"
- regex is supported [[$name =~ *B* ]] && echo "regex can be used"


double square is NOT posix compliant


### Guard clause

Nesting if else statements is a bad practice

The guard clause is a principle to run checks and exit the script such as

if [[ ! -e "${FILE_PATH}" ]] then
    echo "not found"
    exit 1
fi

this also works:
[[ -f "file.txt" ]] || { echo "file does not exist; exit 1;}

while we are here ; is for simple sequencing

### Shebang

sheband should be:

#!/usr/bin/env bash

