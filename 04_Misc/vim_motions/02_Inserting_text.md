`i` - insert text at the cursor  
`I` - insert text at the beginning of the line  

`a` - insert text after the cursor  
`A` - insert text at the end of the line  

`o` - open a new line below the current line and insert  
`O` - open a new line above the current line and insert  

`c` - change (delete and enter insert mode)  
`s` - delete the character under the cursor and enter insert mode  

`yi<parenthesis>` - yank (copy) the text inside the specified parenthesis  
`ya<parenthesis>` - yank the text including the specified parenthesis  

`u` - undo the last change  
`Ctrl + r` - redo the last undone change  

---

`p` - put (paste) the last deleted text after the cursor  
`P` - put the last deleted text before the cursor  

`ciw` - change the entire word under the cursor and replace it  
`ce` - change (delete) from the cursor to the end of the word and enter insert mode  
`c$` - change from the cursor to the end of the line and enter insert mode  
`c^` - change from the cursor to the beginning of the line and enter insert mode  

`.` - repeat the last command  

`/<term>` - search for `<term>` in the file  
`n` - jump to the next occurrence of the search term  
`N` - jump to the previous occurrence of the search term  

---

