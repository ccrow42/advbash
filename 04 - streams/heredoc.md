### Quick Links

-   [Here Documents](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#here-documents)

-   [Basic Principles of Here Documents](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#basic-principles-of-here-documents)

-   [Simple Examples](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#simple-examples)

-   [Handling Tab Characters](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#handling-tab-characters)

-   [Redirecting to a File](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#redirecting-to-a-file)

-   [Piping the Output to Another Command](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#piping-the-output-to-another-command)

-   [Sending Parameters to a Function](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#sending-parameters-to-a-function)

-   [Creating and Sending an Email](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#creating-and-sending-an-email)

-   [Using Here Documents with SSH](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#using-here-documents-with-ssh)

-   [Strange Name, Neat Features](https://www.howtogeek.com/719058/how-to-use-here-documents-in-bash-on-linux/#strange-name-neat-features)

The strangely named "here documents" let you use input/out redirection inside Bash scripts on Linux. They're a great way to automate commands you need to run on a remote computer.

## Here Documents

Many commands in Linux have two or three letter names. This is partly what gives rise to the notion that Linux is hard to learn and full of arcane commands. But one of the weirdest names in Linux isn't one of the cryptically short ones. "Here documents" aren't documents, and it isn't really clear what the "here" refers to, either.

They are a relatively obscure construct, but they are useful. Of course, this is Linux, so there's more than one way to skin a cat. Some of the functionality provided by here documents can be reproduced in other ways. Those alternate methods are usually more complicated. In programming and scripting, "more complicated" also means "more prone to bugs," and that your code is harder to maintain.

Where here documents really excel is in the automation of commands that you want to send to a remote computer from a connection established from within a script. Making the connection is easy, but once the connection has been made, how do you "pump" your commands from your script into the shell on the remote computer? Here documents let you do that very simply.

## Basic Principles of Here Documents

The idiomatic representation of a here document looks like this:

```
COMMAND &lt;&lt; limit_string
        
<p>             .
    </p>    
<p>             .
    </p>    
<p>            text 
    </p>    
<p>            data
    </p>    
<p>            variables
    </p>    
<p>            .
    </p>    
<p>            .
    </p>    
<p>            limit_string</p>
```

-   **COMMAND**: This can be any Linux command that accepts redirected input. Note, the `echo` command [doesn't accept redirected input](https://man7.org/linux/man-pages/man1/echo.1.html). If you need to write to the screen, you can use the `cat` command, [which does](https://man7.org/linux/man-pages/man1/cat.1.html).
-   **<<**: The redirection operator.
-   **limit\_string**: This is a label. It can be whatever you like as long as it doesn't appear in the list of data you're redirecting into the command. It is used to mark the end of the text, data, and variables list.
-   **Data List**: A list of data to be fed to the command. It can contain commands, text, and variables. The contents of the data list are fed into the command one line at a time until the \_limit\_string is encountered.

You'll probably see examples of here documents that use "EOF" as the limit string. We don't favor that approach. It works, but "EOF" means "End of File." Apart from the rare case where a home document is the last thing in a script file, "EOF" is being used erroneously.

It will make your scripts much more readable if you use a limit string that refers to what you're doing. If you're sending a series of commands to a remote computer over [Secure Shell](https://man7.org/linux/man-pages/man1/ssh.1.html) (SSH), a limit string called something like "\_remote\_commands" would make perfect sense. You don't need to start them with an underscore "`_`" character. We do that because it marks them as something out of the ordinary in your script.

## Simple Examples

You can use here documents on the command line and in scripts. When you type the following in a terminal window, you'll see a "`>`" line continuation prompt each time you hit "Enter." When you type the "\_end\_of\_text" limit string and hit "Enter," the list of websites is passed to `cat,` and they are displayed in the terminal window.

```
cat &lt;&lt; _end_of_text 
        
<p>            How-To Geek 
    </p>    
<p>            Review Geek 
    </p>    
<p>            LifeSavvy 
    </p>    
<p>            CloudSavvy&nbsp;IT
    </p>    
<p>            MindBounce
    </p>    
<p>            _end_of_text</p>
```

    ![here document typed on the command line in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/1-3.png)

That's not the most worthwhile of exercises, but it does demonstrate that nothing is sent to the command until the entire list of data is collated and the limit string is encountered. The `cat` command doesn't receive any input until you enter the limit string "\_end\_of\_text" and hit the "Enter" key.

    ![Output from a here document typed on the command line in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/2-2.png)

We can do the same thing in a script. Type or copy this example into an editor, save the file as "heredoc-1.sh", and close the editor.

```
#!/bin/bash
        
<p>            cat &lt;&lt; "_end_of_text"
    </p>    
<p>            Your user name is: $(whoami)
    </p>    
<p>            Your current working directory is: $PWD
    </p>    
<p>            Your Bash version is: $BASH_VERSION
    </p>    
<p>            _end_of_text</p>
```

As you follow this article, each time you create a script, you'll need to [make it executable](https://man7.org/linux/man-pages/man1/chmod.1.html) before it will run. In each case, [use the `chmod` command](https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/). Substitute the name of the script in each example for the script name used here.

```
chmod +x heredoc-1.sh
```

    ![chmod +x heredoc-1.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/3-2.png)

This script contains two environment variables, `$PWD` and `$BASH_VERSION`. The environment variable names are replaced by their data values---the current working directory and the version of Bash---when the script is executed.

The script also uses command substitution on [the `whoami` command](https://www.howtogeek.com/410423/how-to-determine-the-current-user-account-in-linux/). The name of the command is replaced by its own output. The output from the entire script is written to the terminal window by the cat command. We run the script by calling it by name:

```
./heredoc-1.sh
```

    ![Output from ./heredoc-1.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/4-2.png)

If you modify the script and wrap the limit string in the first line of the here document in quotation marks " `"` ", the data list is passed to the here document command verbatim. Variable names are displayed instead of variable values, and command substitution will not take place.

```
#!/bin/bash
        
<p>            cat &lt;&lt;- "_end_of_text"
    </p>    
<p>            Your user name is: $(whoami)
    </p>    
<p>            Your current working directory is: $PWD
    </p>    
<p>            Your Bash version is: $BASH_VERSION
    </p>    
<p>            _end_of_text</p>
```

```
./heredoc-1.sh
```

    ![Output from a modified ./heredoc-1.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/9-2.png)

## Handling Tab Characters

By default, tab characters in your data list will be retained and written to the terminal window. Copy and save this example as "heredoc-2.sh." Make it executable using the `chmod` command. Edit the indented lines to make sure that they have one or two tab characters at the start of the line rather than a series of spaces.

```
#!/bin/bash
        
<p>            cat &lt;&lt; _end_of_text
    </p>    
<p>            Your user name is: $(whoami)
    </p>    
<p>             Your current working directory is: $PWD
    </p>    
<p>             Your Bash version is: $BASH_VERSION
    </p>    
<p>            _end_of_text</p>
```

```
./heredoc-2.sh
```

    ![Output from ./heredoc-2.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/5-2.png)

The tabs are written to the terminal window.

By adding a dash "`-`" to the redirection operator, the here document will ignore leading tab characters. Save this example as "heredoc-3.sh" and make it executable.

```
#!/bin/bash
        
<p>            cat &lt;&lt;- _end_of_text
    </p>    
<p>            Your user name is: $(whoami)
    </p>    
<p>             Your current working directory is: $PWD
    </p>    
<p>             Your Bash version is: $BASH_VERSION
    </p>    
<p>            _end_of_text</p>
```

```
./heredoc-3.sh
```

    ![output from ./heredoc-3.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/15-2.png)

The tabs are ignored. This might seem trivial, but it is a neat way to cope with leading tabs due to indented sections of scripts.

Loops and other logical constructs are usually indented. If your here document is contained in an indented section of a script, using a dash "`-`" with the redirection operator removes formatting issues caused by the leading tab characters.

```
#!/bin/bash
        
<p>            if true; then
    </p>    
<p>             cat &lt;&lt;- _limit_string
    </p>    
<p>             Line 1 with a leading tab.
    </p>    
<p>             Line 2 with a leading tab.
    </p>    
<p>             Line 3 with a leading tab.
    </p>    
<p>             _limit_string
    </p>    
<p>            fi</p>
```

## Redirecting to a File

The output from the command used with the here document can be redirected into a file. Use the "`>`" (create the file) or "`>>`" (create the file if it doesn't exist, append to the file if it does) redirection operators after the limit string in the first line of the here document.

This script is "heredoc-4.sh." It will redirect its output to a text file called "session.txt."

```
#!/bin/bash
        
<p>            cat &lt;&lt; _end_of_text &gt; session.txt
    </p>    
<p>            Your user name is: $(whoami)
    </p>    
<p>            Your current working directory is: $PWD
    </p>    
<p>            Your Bash version is: $BASH_VERSION
    </p>    
<p>            _end_of_text</p>
```

```
./heredoc-4.sh
```

```
cat session.text
```

    ![Output from ./heredoc-4.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/6-2.png)

## Piping the Output to Another Command

The output from the command used in a here document can be piped as the input to another command. Use [the pipe "`|`" operator](https://www.howtogeek.com/438882/how-to-use-pipes-on-linux/) after the limit string in the first line of the here document. We're going to pipe the output from the here document command, `cat`, into `sed`. We want to [substitute all occurrences](https://man7.org/linux/man-pages/man1/sed.1.html) of the letter "a" with the letter "e".

Name this script "heredoc-5.sh."

```
#!/bin/bash
        
<p>            cat &lt;&lt; _end_of_text | sed 's/a/e/g'
    </p>    
<p>            How
    </p>    
<p>            To
    </p>    
<p>            Gaak
    </p>    
<p>            _end_of_text</p>
```

```
./heredoc-5.sh
```

"Gaak" is corrected to "Geek."

    ![Output from ./heredoc-5.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/7-2.png)

## Sending Parameters to a Function

The command that is used with a here document can be a function in the script.

This script passes some vehicle data into a function. The function reads the data as though it had been typed in by a user. The values of the variables are then printed. Save this script as "heredoc-6.sh".

```
#!/bin/bash
        
<p>            # the set_car_details() function
    </p>    
<p>            set_car_details ()
    </p>    
<p>            {
    </p>    
<p>            read make
    </p>    
<p>            read model
    </p>    
<p>            read new_used
    </p>    
<p>            read delivery_collect
    </p>    
<p>            read location
    </p>    
<p>            read price
    </p>    
<p>            }
    </p>    
<p>            # The here document that passes the data to set_car_details()
    </p>    
<p>            set_car_details &lt;&lt; _mars_rover_data
    </p>    
<p>            NASA
    </p>    
<p>            Perseverance Rover
    </p>    
<p>            Used
    </p>    
<p>            Collect
    </p>    
<p>            Mars (long,lat) 77.451865,18.445161
    </p>    
<p>            2.2 billion
    </p>    
<p>            _mars_rover_data
    </p>    
<p>            # Retrieve the vehicle details
    </p>    
<p>            echo "Make: $make"
    </p>    
<p>            echo "Model: $model"
    </p>    
<p>            echo "New or Used: $new_used"
    </p>    
<p>            echo "Delivery or Collection: $delivery_collect"
    </p>    
<p>            echo "Location: $location"
    </p>    
<p>            echo "Price \$: $price"</p>
```

```
./heredoc-6.sh
```

    ![Output from ./heredoc-6.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/8-1.png)

The vehicle details are written to the terminal window.

## Creating and Sending an Email

We can use a here document to compose and send an email. Note that we can pass parameters to the command in front of the redirection operator. We're [using the Linux `mail` command](https://www.howtogeek.com/devops/how-to-set-up-a-mail-agent-for-command-line-email/) to [send an email through the local mail system](https://linux.die.net/man/1/mail) to the user account called "dave". The `-s` (subject) option allows us to specify the subject for the email.

This example forms script "heredoc-7.sh."

```
#!/bin/bash
        
<p>            article="Here Documents"
    </p>    
<p>            mail -s 'Workload status' dave &lt;&lt; _project_report
    </p>    
<p>            User name: $(whoami)
    </p>    
<p>            Has completed assignment:
    </p>    
<p>            Article: $article
    </p>    
<p>            _project_report</p>
```

```
./heredoc-7.sh
```

    ![./heredoc-7.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/10-1.png)

There is no visible output from this script. But when we check our mail, we see that the email was composed, dispatched, and delivered.

```
mail
```

    ![Output from the mail command in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/11-2.png)

## Using Here Documents with SSH

Here documents are a powerful and convenient way to execute some commands on a remote computer once an SSH connection has been established. If you've set up SSH keys between the two computers, the login process will be fully automatic. In this quick and dirty example, you'll be prompted for the password for the user account on the remote computer.

This script is "heredoc-8.sh". We're going to connect to a remote computer called "remote-pc". The user account is called "dave". We're using the `-T` (disable pseudo-terminal allocation) option because we don't need an interactive pseudo-terminal to be assigned to us.

In the "do some work in here" section of the script, we could pass a list of commands, and these would be executed on the remote computer. Of course, you could just call a script that was on the remote computer. The remote script could hold all of the commands and routines that you want to have executed.

All that our script---heredoc-8.sh---is going to do is update a connection log on the remote computer. The user account and a time and date stamp are logged to a text file.

```
#!/bin/bash
        
<p>            ssh -T dave@remote-pc.local &lt;&lt; _remote_commands
    </p>    
<p>            # do some work in here
    </p>    
<p>            # update connection log
    </p>    
<p>            echo $USER "-" $(date) &gt;&gt; /home/dave/conn_log/script.log
    </p>    
<p>            _remote_commands</p>
```

When we run the command, we are prompted for the password for the account on the remote computer.

```
./heredoc-8.sh
```

    ![./heredoc-8.sh and a password prompt in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/12-2.png)

Some information about the remote computer is displayed, and we're returned to the command prompt.

    ![Output from ./heredoc-8.sh in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/13-1.png)

On the remote computer, we can use `cat` to check the connection log:

```
cat conn_log/script.log
```

    ![cat conn_log/script.log in a terminal window](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/2021/03/14-2.png)

Each connection is listed for us.

## Strange Name, Neat Features

Here documents are quirky but powerful, especially when used to send commands to a remote computer. It'd be a simple matter to script a backup routine using `rsync`. The script could then connect to the remote computer, check the remaining storage space, and send an alerting email if space was getting low.
