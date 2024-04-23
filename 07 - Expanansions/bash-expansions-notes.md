## Expansions - Part Two


### Brace expansion

`touch sample{a..c}`
can be acending or decending

`touch {MKT,DEV}{1..3}`

`echo file{1..10..2}.txt`
Step based expasnion


```
for i in {1..3}; do touch "file${i}.txt"; done
```

### Command substitution expansion

```
file_count=$(find . -type f | wc -l)
```
don't use back-ticks for command substitution

the above is an example of a subshell. Subshells do not propigate variables back to the shell.

### Subshell

any code in () is in a subshell

when do we use them?

- When we want to run commands in a different directory

**NOTE: Propigate a value back to the parent**

```
tmpfile="/tmp/$$.tmp"
counter=1
echo "${counter}" > ${tmpfile}
(
counter="$(($(cat ${tmpfile}) + 1 ))"
echo "${counter" > ${tmpfile}
)

counter=$(cat ${tmpfile})

echo "${counter}"

unlink "${tmpfile}"
```



