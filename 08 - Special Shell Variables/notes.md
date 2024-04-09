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




