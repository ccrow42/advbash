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
s - substitutes text
a - add text
i - inserttext
