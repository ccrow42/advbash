### Expansions

### Variables

So far a bit basic. Variables should be lower case.

again, use {} around var names ${varname}. They can also sting manuiplation or default values:

```
echo "Hello ${name:-Unknown}
```

Unknown will be the value of the variable if it doesn't have a value.

**Subscring var expansions:**
```
name="John Doe"
echo "Hello, ${name:0:4}"
```
Will just print John

**Substring substitution:**
```
path="/home/user/file.txt"
echo "${path/file/data}"
```
will print /home/user/data.txt

We can get the length of a variable using:
```
echo "${#name}"
```

It is also important to use "" for evaluations.


### Parameter - Part One

`# prefix`

`# suffix`

```
greetings="Hello world"
echo "${greetings#H}"
```
Prefix match MUST MATCH, so we could have: `"${greetings#Hello}`

% works the same way.


### Part 2

`*` is a glob

```
export position1="Senior Cloud Architect"
echo "${position1#* }"
```

```
my_text_file="/home/my_username/text_file.txt"
my_pithon_file="/usr/bin/app.py"

echo "${my_text_file##*/}"
echo "${my_pithon_file%.*}"

# best practice is to use longest for dir path and shortest for suffix
```

# or % shortest prefix or suffix removal

## or %% longest prefix or suffix removal
