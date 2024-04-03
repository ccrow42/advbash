Recently, I covered [how you can use the number of arguments in bash](https://linuxhandbook.com/bash-number-arguments/) that involved the use of the `$#` variable which is one of the special variables of bash.

And in this guide, I will walk you through all of those special bash variables. I will share scripting examples in the later part of this tutorial.

## Special variables in bash

Here's quick look into the special variables you get in bash shell:

| Special Variable | Description |
| --- | --- |
| `$0` | Gets the name of the current script. |
| `$#` | Gets the number of arguments passed while executing the bash script. |
| `$*` | Gives you a string containing every command-line argument. |
| `$@` | It stores the list of every command-line argument as an array. |
| `$1-$9` | Stores the first 9 arguments. |
| `$?` | Gets the status of the last command or the most recently executed process. |
| `$!` | Shows the process ID of the last background command. |
| `$$` | Gets the process ID of the current shell. |
| `$-` | It will print the current set of options in your current shell. |

Now, let's have a look at them one by one in detail.

### $0: Get the name of the script

To get the name of the current script, you will have to utilize the `#0` variable in your script with the echo.

For example, here, I created a simple hello world program named `Hello.sh` which should reflect the filename while executing:

```
#!/bin/bash
echo "Hello from sagar"
echo "Name of shell script = $0"
```

And here's the output it gave while running:

![Get the name of the current script in Linux using special variable](https://linuxhandbook.com/content/images/2023/03/Get-the-name-of-the-current-script-in-Linux-using-special-variable.png)

### $#: Get the number of arguments passed to the bash script

So if you want the number of arguments passed to the bash script while executing, you will have to include the `$#` variable to your script.

For your reference, here, I made a simple hello world program that includes the `$#` variable:

```
#!/bin/bash
echo "Hello from sagar"
echo "Number of arguments passed to this script = $#"
```

To put this script to the test, I passed 3 arguments while executing the script:

![Get the number of arguments passed to the bash script](https://linuxhandbook.com/content/images/2023/03/Get-the-number-of-arguments-passed-to-the-bash-script.png)

And as you can see, it gave me an accurate number of passed arguments.

### $\*: Get the string of passed arguments to the bash script

So if you want to get the string of passed arguments to the bash script, all you have to do is include the `$*` in that script.

And for your reference, I have made a simple script:

```
#!/bin/bash

echo "Number of arguments=${#*}"
echo

for arg in "$*"
do
        echo "$arg "
done
```

Once you make shown changes, you can pass desired arguments, and it will show the total number of passed arguments and the name of every argument:

![](https://linuxhandbook.com/content/images/2023/03/Get-the-string-of-passed-arguments-to-the-bash-script.png)

### $@: Get the list of passed arguments to the bash script

Think of this as an advanced form of the above example where you also get the name of the passed arguments in a column.

Here, I created a simple script that will give you the total number of arguments and the list of passed arguments:

```
#!/bin/bash
echo "No of arguments=${#@}"

echo

for arg in "$@"
do
        echo "$arg "
done
```

And when I executed the script with five arguments, it should print all of them, including their count:

![get the number of passed arguments to the bash script](https://linuxhandbook.com/content/images/2023/03/get-the-number-of-passed-arguments-to-the-bash-script.png)

### $n: Store the first nine arguments of the bash script

⚠️

Using this method, you can not store more than 9 arguments.

In this method, you will be using different variables to store arguments so for some users this might not be the most efficient way.

But if you decide to go with this method, here's how the syntax should be:

```
#!/bin/bash
echo "Hello world"

# Use desired number of variables (till 9)
echo Argument 1 = $1
echo Argument 2 = $2
echo Argument 3 = $3
echo Argument 4 = $4
```

Once done, you can execute the script and pass arguments (up to the number of declared variables):

![use variables to store passed arguments in bash script](https://linuxhandbook.com/content/images/2023/03/use-variables-to-store-passed-arguments-in-bash-script.png)

### $?: Get the status of the last execution in bash

So if you want to check the status of the last command execution, you can use the `$?` variable in your terminal directly.

Here,

-   `0` indicates success
-   `1` indicates failure

You can also get something else than `0` or `1` such as:

`127` which indicates the error code for the command not found.

You can use the `$?` variable in your terminal as shown:

```
echo $?
```

![get the exit status of the last execution in linux](https://linuxhandbook.com/content/images/2023/03/get-the-exit-status-of-the-last-execution-in-linux.png)

In conclusion, anything else than `0` indicates the failure in execution!

### $!: Get the PID of the most recent active execution

Using this method, you can get the PID of the most recent command execution that is currently running in the background.

To use this variable, you will have to use the `$!` variable with echo:

```
echo $!
```

![get PID of the most recent active in background](https://linuxhandbook.com/content/images/2023/03/get-PID-of-the-most-recent-active-in-background.png)

And as you can see, for me, it was `2562`. Also, if you want, you can use the PID to kill the process in Linux:

### $$: Get the PID of the current shell

So if you want to know the PID of the current shell, all you have to do is use the `$$` variable in the terminal:

```
echo $$
```

![get the PID of the current shell](https://linuxhandbook.com/content/images/2023/03/get-the-PID-of-the-current-shell.png)

### $-: Find the set of options used in the current shell

You can set various options to tweak how the bash should behave and using the `$-` variable, you can print the currently enabled options:

```
echo $-
```

![find active options in bash using the $- variable](https://linuxhandbook.com/content/images/2023/03/find-active-options-in-bash-using-the----variable.png)

Seems confusing. Isn't it? Let me interpret it for you.

Here,

-   `h` (hashall): Using this option, bash is instructed to keep track of every command location it has discovered while searching your PATH.
-   `i` (interactive): This means your current shell is interactive.
-   `m` (monitor): This option enables job control.
-   `B` (braceexpand): Enables the [brace expansion](https://linuxhandbook.com/brace-expansion/).
-   `H`: (histexpand): This option enables you to re-run the command from the history by placing the number after the exclamation (`!number`).
-   `s` (source command from stdin): If this option is present, the commands are read from the standard input.

## Varied variety of variables

You can use variables in bash script like most scripting languages.

These special variables give you more control over the script.

Apart from these special variables, there are also environment variables in bash. A little about changing them in this tutorial.

I hope you will find this guide helpful. If you have any doubts or suggestions, feel free to ask in the comments.
