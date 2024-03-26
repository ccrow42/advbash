## **Vim the hard way**

https://learnvim.irian.to/read_this_first

### Buffers

You can have multiple files open

`vim file1 file2`

This will load the files in to a buffer.

:buffers will show a list of files

:bnext and :bprevious
:buffer + *n*
:buffer 2
:bdelete

you can close all by adding the all command to extended command mode:
:qall
:qall!
:wqall

### windows

We can split a window with 
:split
:vsplit

move with ^w and arrow keys

### Tabs

:tabnew
:tabclose
:tabnext
:tabprevious

I haven't played with this at all


### Navigation
w     Move forward to the beginning of the next word
W     Move forward to the beginning of the next WORD
e     Move forward one word to the end of the next word
E     Move forward one word to the end of the next WORD
b     Move backward to beginning of the previous word
B     Move backward to beginning of the previous WORD
ge    Move backward to end of the previous word
gE    Move backward to end of the previous WORD

0 and $

:g/pattern/command

:g!/pattern/command

i    Insert text before the cursor
I    Insert text before the first non-blank character of the line
a    Append text after the cursor
A    Append text at the end of line
o    Starts a new line below the cursor and insert text
O    Starts a new line above the cursor and insert text
s    Delete the character under the cursor and insert text
S    Delete the current line and insert text
gi   Insert text in same position where the last insert mode was stopped
gI   Insert text at the start of line (column 1)

h   Left
j   Down
k   Up
l   Right



### Registers

There is a lot of info about registers, but it is like the hp calculators.

using yy puts things in to the yank register

numbered registers fill in sequential order

the `.` command updates the register number.

"" is yank, so recall with ""p

you can use a numbered register with "1p "2p etc

repeats count as a single command, so 3dd puts 3 lines in the first register

Deleting less than a line goes in to the small delete register "-p
