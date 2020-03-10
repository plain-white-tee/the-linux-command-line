https://www.linux.com/tutorials/vim-101-beginners-guide-vim/ 
`h` moves the cursor one character to the left.<br>
`j` moves the cursor down one line.<br>
`k` moves the cursor up one line.<br>
`l` moves the cursor one character to the right.<br>
`0` moves the cursor to the beginning of the line.<br>
`$` moves the cursor to the end of the line.<br>
`w` move forward one word.<br>
`b` move backward one word.<br>
`G` move to the end of the file.<br>
`gg` move to the beginning of the file.<br>
`` `.`` move to the last edit.

Here’s a handy tip: prefacing a movement command with a number will execute that movement multiple times.<br>
So, if you want to move up six lines, enter `6k` and Vim will move the cursor up six lines. If you want to move over five words, enter `5w`. To move 10 words back, use `10b`.

`d` starts the delete operation.<br>
`dw` will delete a word.<br>
`d0` will delete to the beginning of a line.<br>
`d$` will delete to the end of a line.<br>
`dgg` will delete to the beginning of the file.<br>
`dG` will delete to the end of the file.<br>
`u` will undo the last operation.<br>
`Ctrl-r` will redo the last undo.

`/text` search for text in the document, going forward.<br>
`n` move the cursor to the next instance of the text from the last search. This will wrap to the beginning of the document.<br>
`N` move the cursor to the previous instance of the text from the last search.<br>
`?text` search for `text` in the document, going backwards.<br>
`:%s/text/replacement text/g` search through the entire document for text and replace it with replacement text.<br>
`:%s/text/replacement text/gc` search through the entire document and confirm before replacing text.<br>
[Here is a handy reference for regular expressions in vim.](https://learnbyexample.gitbooks.io/vim-reference/content/Regular_Expressions.html)<br>
Confirmation options:<br>
replace with 'replacement text' (y/n/a/q/l/^E/^Y)?<br>
`y` confirm substitution.<br>
`n` skip this instance of substitution.<br>
`a` substitute this and all subsequent matches.<br>
`q` or `ESC` quit.<br>
`l` substitute this instance and then quit.<br>
`CTRL-E`, `CTRL-Y` scroll down and up.

`v` highlight one character at a time.<br>
`V` highlight one line at a time.<br>
`Ctrl-v` highlight by columns.<br>
`p` paste text after the current line.<br>
`P` paste text on the current line.<br>
`yy` copy the current line.<br>
`yw` will delete a word.<br>
`y0` will delete to the beginning of a line.<br>
`y$` will delete to the end of a line.

`o` open the line below current line.<br>
`O` open the line below current line.<br>
`a` append.<br>
`A` append at end of line.<br>
`J` join current line with the line below it.

`:n` switch to next file.<br>
`:N` switch to previous file.<br>
`:buffers` list open files.<br>
`:buffer [n]` switch to file `[n]`.<br>
`:e [filename]` open `[filename]` for editing.<br>
`:r [filename]` reads `[filename]` into current editor.<br>
`:w filename` - write to `filename`<br>
`:q` - quit<br>
`ZZ` write file and quit

