### sed introduction

`sed 's/sample/are/g' poem.txt

s - substitute 
g - global

### sed print
p - prints the input line without modification.
`sed 'p' testfile.txt` will print the contents testfile.txt twice (once unmodified, and once modified)

`sed '2p' testfile.txt` will process (and print) the entire file but will only "process" the second line

-n supresses automatic line printing, so only the processed data prints

d - deletes text
s - substitute
a - add text
i - inserttext

### sed delete

sed '5d' employees.txt

sed '3,5d' employees.txt # deletes a range

-i modify in place. Will not output to the terminal

### search
'/word-to-search/' it requries a command
we need a command so

sed -n '/Manager/p' employees.txt

sed -n '/\bMa\b/p' employees.txt

we can add multiple patterns:
`sed -n -e '/\bManager\b/p' -e '/\bIT\b/p' employees.txt` this is additive

`sed -e '/\bMa\b/d' employees.txt`

### substitute

didn't seem to launch...


### Advanced examples

Using sed to remove ansi characters:
sed -e 's/\x1b\[[0-9;]*m//g;s/[][():\+\%\!\=\"]//g' "${log}"

find the participant id and load it in to a variable:
local participant_id=$(sed -n 's/.*Participant\ ID\:\ \(\w\{12\}\).*/\1/p' ${log})

# Sample input data
input_data="2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 02:cb:0c:c4:15:07 brd ff:ff:ff:ff:ff:ff
    inet 192.168.48.27/19 brd 192.168.63.255 scope global dynamic eth0
       valid_lft 2441sec preferred_lft 2441sec
    inet6 fe80::cb:cff:fec4:1507/64 scope link"

# Use sed to extract the IP address
output_data=$(echo "$input_data" | sed -n -E 's/.*inet[[:space:]]+([0-9]+\.[0-9]+\.[0-9]+\.[0-9]+).*/\1/p')

# Print the result
echo "$output_data"

the above will pull out an IP address. -E enables extended regular expressions
