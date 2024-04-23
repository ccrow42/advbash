# Special shell variables

### $?

returns the exit code

There are some reserved exit codes:
- 0 - success
- 1 - general error
- 2 - misuse of shell built-ins
- 126 - cannot execute
- 127 - command not found
- 128 or 130 script terminated by ^c


Some examples

```
if [[ ! $? -eq 0 ]]; then
  echo "error"
  exit1
fi
```

```
ehco "hello" || { echo "error"; exit 1; }
```

a better strategy would be to add:

```
set -e

ehco "Hello!"

exit 0


```

### Generic terminate function

```
#!/usr/bin/env bash
set -e

readonly ERROR_CONF_FILE=150

terminate () {
  Local msg="${1}"
  Local code="${2:-160}"
  echo "Error: ${msg}" >&2
  exit "${code}
}

if [[ ! -s "${CONF_FILE}" ]]; then
  terminate "Generic error message" "${ERROR_CONF_FILE}"
fi

exit 0
```


### $#

Holds the number of arguments passed

Can be used to ensure that a required number of arguments are passed.

```

#!/usr/bin/env bash
if [[ $# -ne 1 ]]; then
  terminate "Please pass one argument" "${CL_ARGS_ERROR}"
fi
```

- use -ne so that we get the exact number of args
- use -lt for a minimum args guard clause

### ifs

an environment variable that contains the seperators for an element

Ansi-C quoting block


We can change the seperator:

```

IFS=":"

elements = "element1:element2:element3"
for element in elements; do
  echo "${element} is a value"
done
```

We can also use the set command pass values in variables as args (and indeed, IFS changes that seperator)

```
IFS=","
val="one,two,three"
set -- ${val}
echo $1
```

### Args

`$* and $@`

`$@` iterable elements for loops

`$*` in a single string seperated by the first IFS seperator

These should be expanded with double quotes 

IFS=',' will replace the seperateor in `$*`

**REMEMBER** the IFS var in a script only affects the expansion of a variable, so it MUST be re-assigned.


### pid


$! gets the pid of the last command that was sent to the background

$$ stores the pid of the current shell or script that it is being executed from

subshells inherit variables from their parent, including $$

### Zero ($0)

It can
- Get the name of the script
- Get the directory

eg

`readonly SCRIPT_NAME=${0##*/}`

This can be used for a usage block:

```
#!/usr/bin/env bash
readonly SCRIPT_NAME=${0##*/}

usage() {
  cat <<USAGE
Usage: ${SCRIPT_NAME} <name>
This script greets the user with teh porvided name.
Arguments:
  name	The name of the user to greet
Options
  -h, --help show this help message and exit
USAGE
}

if [[ $# -ne 1 ]]; then
  usage
  exit 1
fi

if [[ "${1}" == "-h" ]] || [[ "${1}" == "--help" ]]; then
  usage
  exit 0
fi

name ] "${1}"
echo "Hello, ${name}! Welocme to the example script!"
exit 0
```
eg to get the absolute path of the script

```
readonly WORK_DIR=$(dirname $(readlink -f "$0"))
readonly SCRIPT_NAME="${$0##/*}"

cd "${WORK_DIR}/.."
```

### Underscore $_

Mostly used for interactive shells

Returns the *last* argument of the last command

```
ls -l file.conf
cp $_ /tmp
```

### Dash $-

options or flags from the current shell

