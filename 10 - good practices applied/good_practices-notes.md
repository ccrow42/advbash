### Strict Mode

set -e # exits on error
set -u # exits when an unset variable is used
set -o pipefail # catches errors in piped commands


example for catching pipefails

```
set -euo pipefail
# needs terminate function
cat non-existent-file.txt | sort || { terminate "Error in piped command" "${PIPE_ERROR}"; }
```


### NO-OP Commands

is useful for dry runs

it is a placeholder shell command

```
if [[ "$1" = "start" ]]; then
    :
else
    echo "Invalid command."
fi
```

it can look cleaner.

### Comments

### Logging

```
log () {

    echo $(date -u +"%Y-%m-%dT%H:%M:%SZ") "${@}"
}

log "hello world!!"
```


