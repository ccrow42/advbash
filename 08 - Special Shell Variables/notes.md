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


