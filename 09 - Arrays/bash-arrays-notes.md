### Declare

There is a string and a int. If the value is surrounded by quotes, it is a string, otherwise it is an int.

Even if a variable is surrounded by double quotes it can be treated as a string

This is Dynamically Typed Syntax

declare provides some control:

```
declare -i i=10

echo $(($i+1))

i="hello" # This will store a 0

declare -a # declares an array
declare -A #associative array
declare -r r_var="ReadOnly" # throws an error (some as readonly)
declare -u uppercase="String"
declare -l lowercase="String
```


### Arrays

array[0]="First Element"
array[1]="Second Element"

echo "${array[0])"
echo "${array[@]}"

Use double quotes in arrays, otherwise spaces and other characters in the element will be interated over.

You can also declare with:
array=("First Element" "Second Element")
remember, the elements are seperated by the $IFS var

declare -a array=("First Element" "Second Element")
array="overwrites only first element"
echo "${array[@]}"

### Insert

${#servers[@]} returns the elements count in an array. The count starts from 1, so

servers[${#servers[@]}]="server4"

To insert in the middle of the array
${servers[@]:0:1}
# find a slice starting at index 0 and return 1 value

eg

```
servers=("server1" "server2" "server3")
servers=( "${servers[@]:0:1" "server1.5" "${servers[@]:1}" )
# the above will insert server 1.5

### Remove elements

declare - a servers("server1" "server2" "server3"}
unset servers[1]

Bash will automatically re-arranges the values, so 

unset servers #removes all elements


### Sort

```
declare -a array=("One" "Two" "Three")
array+=("Four" "Five" "Six")

# Bash has a sort command
# The sort command must have data in multiple lines

printf "%s\n" d e a b | sort

printf "%s\n" "${array[@]}" | sort

```

### Associative arrays

```
declare -A chest_drawer=( ["shirts"]="T-shirts and polo shirts" ["sports"]="All sorts of sports clothes" )

echo "${chest_drawer["shirts"]}"
```

Unset works with associative arrays
`unset chest_drawer["shirts"]

print key name with `echo "${!chest_drawer[@]}" Use this with a for loop
