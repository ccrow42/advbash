### Coding convensions

**Variables**

lower case with _ as seperator: user_address

Should be descriptive, and not short-hand.

Constants:
  readoly file = "filename" : ensures the file cannot be changed.

export is used for vars that will be used outside the script: export message = "Hello"


**Functions**

lower case with _ as seperator: calculate_area()

example:

```
calculate_area() {

}
```

**Expanding Variables**

$ indicates a value that can be accessed or utilied

```
var="value of var"
echo ${var}
```

We could have just used `$var`, however:

```height=170

echo "height is = $heightcm" # will not work
echo "height is = ${height}cm # will work

Generally use double quetes to expand variables. If the variable contains seperators, we could have some uninteded consiquences. For example:


```
string="One Two Three"
for element in ${string}; do
  echo ${element}
done

# will display:
# one
# two
# three

#but we could have used:
for element in "${string}"; do
  echo ${element}
done

#Will display:
# one two three

So which is right? It depends, but use for the following:
- directory paths, filenames
- assigning URLs to vars
- When in doubt



