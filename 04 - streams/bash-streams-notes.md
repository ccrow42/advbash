### Overview

streams refer to the flow of data.

There are 3 streams in linux:
- stdin - 0
- stdout - 1
- stderr - 2

They can be redirected

> output
< input
| pipe

### stdout stderr

> is standard out by default
2> will redirect standard err

the numbers are called file descriptors

for example, we can use this:
ls -z > stdout.txt 2>stderr.txt


### file descriptors

there are more that 3 file descriptors and they can reference files or sockets

### /dev/null

We are going to explain what 2>&1 does (my guess is that in redirects stderr to stdout)

& before the redirect is a wildcard to match both stdout and stderr, for example
ls -l &> out.txt # this will capture both stderr and stdout in to the out.txt file.

When on the right side of the redirect, & pushes to a file descriptor (think about what would happen with out the &, it would assume that we are pushing to a file called 1

The final destination should be added right after the command, for example:
ls -z > file.txt 2>&1 would be correct.

### Input

stdin or file descriptor 0

stdinput

| anon pipe or just a pipe

^d signals the end of input

We can open an additional file descriptor by using the exec command
```
echo "Joan Carlos@Kodekloud.com" >email_file.txt
exec 3<> email_file.txt
read -n 4 <&3
echo -n "." >&3
exec 3>&-
```

### heredocs

this tool will create a multiline text file

```
cat > file.txt <<EOF
line1
line2
line3
EOF

cat <<EOF
test1
text2
EOF

cat <<EOF | k apply -f -
yaml
yaml
EOF

ssh ubuntu@server <<EOF
many commands
commands
commands
EOF

cat <<- EOF
	this will ignore tabs
EOF

cat << "EOF"
This will not expand $VARS
EOF

```



There is also a herestrings:

`cat <<< "Hello World"`

### Pipes

Named pipes use < and >

```
sort abc.txt > abc_soorted.txt
```

| is an anonymous pipe. Can chain togother multiple commands.

sort and uniq are interesting text processing commands

pipes ignore stderr

### pipefail

echo $? will print the exit status of the last command

set -o pipefail will exit the pipe.

It is also a best practice to exit out of the script with an error, eg
`sort somefile.txt | uniq || exit 80`

exit 80 will only trigger if the pipe fails (instead of moving on to the next command.

set -o noclobber


### exit-code

### xargs

xargs takes \n tab and space characters and sends the strings as arguments to the command, that it runs repeatedly. It can save some complex looping

eg:
` cat file.txt | xargs echo`

echo "dir1 dir2 dir3" | xargs mkdir

### eval

no clue...

` eval 'echo "Hello!!"' `

It can be used to run a command stored in a variable:

```
cmd="ls -l"

eval $cmd
```

be careful with eval as it will execute based on vars, without input sanitization we will have code injection vulnerabilty.

We could instead use subshells


### printf

can format texit in a specific way. 
types:
- %d integers
- %f float
- %s strings

it supports newline \n and tab \t

```
name="John"
age=30
weight=78.5

printf "My name is %s, I am %d years old and my weight is %.1f kg.\n" $name $age $weight
```

it is a posix standard
