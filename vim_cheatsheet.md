https://www.linux.com/tutorials/vim-101-beginners-guide-vim/ 
`h` moves the cursor one character to the left.
`j` moves the cursor down one line.
`k` moves the cursor up one line.
`l` moves the cursor one character to the right.
`0` moves the cursor to the beginning of the line.
`$` moves the cursor to the end of the line.
`w` move forward one word.
`b` move backward one word.
`G` move to the end of the file.
`gg` move to the beginning of the file.
`` `.`` move to the last edit.

Here’s a handy tip: prefacing a movement command with a number will execute that movement multiple times.
So, if you want to move up six lines, enter `6k` and Vim will move the cursor up six lines. If you want to move over five words, enter `5w`. To move 10 words back, use `10b`.

`d` starts the delete operation.
`dw` will delete a word.
`d0` will delete to the beginning of a line.
`d$` will delete to the end of a line.
`dgg` will delete to the beginning of the file.
`dG` will delete to the end of the file.
`u` will undo the last operation.
`Ctrl-r` will redo the last undo.

`/text` search for text in the document, going forward.
`n` move the cursor to the next instance of the text from the last search. This will wrap to the beginning of the document.
`N` move the cursor to the previous instance of the text from the last search.
`?text` search for `text` in the document, going backwards.
`:%s/text/replacement text/g` search through the entire document for text and replace it with replacement text.
`:%s/text/replacement text/gc` search through the entire document and confirm before replacing text.
[Here is a handy reference for regular expressions in vim.](https://learnbyexample.gitbooks.io/vim-reference/content/Regular_Expressions.html)
Confirmation options:
replace with 'replacement text' (y/n/a/q/l/^E/^Y)?
`y` confirm substitution.
`n` skip this instance of substitution.
`a` substitute this and all subsequent matches.
`q` or `ESC` quit.
`l` substitute this instance and then quit.
`CTRL-E`, `CTRL-Y` scroll down and up.

`v` highlight one character at a time.
`V` highlight one line at a time.
`Ctrl-v` highlight by columns.
`p` paste text after the current line.
`P` paste text on the current line.
`yy` copy the current line.
`yw` will delete a word.
`y0` will delete to the beginning of a line.
`y$` will delete to the end of a line.

`o` open the line below current line.
`O` open the line below current line.
`a` append.
`A` append at end of line.
`J` join current line with the line below it.

`:n` switch to next file.
`:N` switch to previous file.
`:buffers` list open files.
`:buffer [n]` switch to file `[n]`.
`:e [filename]` open `[filename]` for editing.
`:r [filename]` reads `[filename]` into current editor.
`:w filename` - write to `filename`
`:q` - quit
`ZZ` write file and quit