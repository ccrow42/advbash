### Useful (I hope) links

https://www.freecodecamp.org/news/vim-beginners-guide/


#### vim beginners guide notes

**Copy and Paste**

at the start of the text you want to copy press 'v'
highsight the text
press `y` to copy and 'd' to cut
this will exit visual mode
press `p` or `P` to paste


**Find and replace**

`[range]s/{pattern}/{string}/[flags]`

range: % to replace all lines, or to look at a selection 5,10. You can also pass . for current or $ for previous

{pattern} regex to find text

{string} what we are replacing with

[flags] 
o to confirm before replacing
i case-insensitive
g for all instances (global IIRC)

**Undo and Redo**
u to undo
^R to redo

**Misc Editing**
a number in command mode will repeat the next command
d for delete
dd for delete line
dw for delete word




