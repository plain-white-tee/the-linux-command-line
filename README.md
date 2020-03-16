# Notes and files for [The Linux Command Line](http://linuxcommand.org/tlcl.php)

***

## Part 4 - Writing Shell Scripts

### 26 - Top-Down Design

#### Shell Functions

```
name () {
    commands
    return
}
```

#### Local Variables
defined with the `local` keyword.

```
funct_1 () {
    local foo # variable foo local to funct_1
      
    foo=1
}
```
    
##### Shell Functions in `.bashrc`

Shell functions are preferred over aliases.
You can add this to `.bashrc` to report disk space.

```
ds () {
    echo "Disk Space Utilization For $HOSTNAME"
    df -h
}
```

### 27 – Flow Control: Branching with if

```
x=5
if [ "$x" -eq 5 ]; then
    echo "x equals 5."
else
    echo "x does not equal 5."
fi
```

On the command line:
`x=5`<br>
`if [ “$x” -eq 5 ]; then echo "equals 5"; else echo "does not equal 5"; fi`

#### Exit Status

`$?` parameter holds the exit status of the last command.<br>
`0` always means success. Any other number `1-255` means failure.<br>
`true` command always executes successfully.<br>
`false` command always executes unsuccessfully.

The `if` statement really only evaluates the exit status of commands.<br>
`if true; then echo "It's true."; fi`

#### test

The `test` command performs checks and comparisons.<br>
Most common form is:
`[ expression ]`

##### File Expressions

| Expression      | Is True If...                                                                                                                                 |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| file1 -ef file2 | file1 and file2 have the same inode numbers (the two filenames refer to the same file by hard linking).                                       |
| file1 -nt file2 | file1 is newer than file2.                                                                                                                    |
| file1 -ot file2 | file1 is older than file2.                                                                                                                    |
| -b file         | file exists and is a block-special (device) file.                                                                                             |
| -c file         | file exists and is a character-special (device) file.                                                                                         |
| -d file         | file exists and is a directory.                                                                                                               |
| -e file         | file exists.                                                                                                                                  |
| -f file         | file exists and is a regular file.                                                                                                            |
| -g file         | file exists and is set-group-ID.                                                                                                              |
| -G file         | file exists and is owned by the effective group ID.                                                                                           |
| -k file         | file exists and has its “sticky bit” set.                                                                                                     |
| -L file         | file exists and is a symbolic link.                                                                                                           |
| -O file         | file exists and is owned by the effective user ID.                                                                                            |
| -p file         | file exists and is a named pipe.                                                                                                              |
| -r file         | file exists and is readable (has readable permission for the effective user).                                                                 |
| -s file         | file exists and has a length greater than zero.                                                                                               |
| -S file         | file exists and is a network socket.                                                                                                          |
| -t fd           | fd is a file descriptor directed to/from the terminal. This can be used to determine whether standard input/output/error is being redirected. |
| -u file         | file exists and is setuid.                                                                                                                    |
| -w file         | file exists and is writable (has write permission for the effective user).                                                                    |
| -x file         | file exists and is executable (has execute/search permission for the effective user).                                                         |

The script `test-file` demonstrates `test`.

##### String Expressions

| Expression         | Is True If...                                                                                                 |
|--------------------|---------------------------------------------------------------------------------------------------------------|
| string             | string is not null.                                                                                           |
| -n string          | The length of string is greater than zero.                                                                    |
| -z string          | The length of string is zero.                                                                                 |
| string1 = string2  | string1 and string2 are equal. Single or double equal signs may be used.                                      |
| string1 == string2 | The use of double equal signs is supported by bash and is generally preferred, but it is not POSIX compliant. |
| string1 != string2 | string1 and string2 are not equal.                                                                            |
| string1 > string2  | string1 sorts after string2.                                                                                  |
| string1 < string2  | string1 sorts before string2.                                                                                 |

The script `test-string` demonstrates string evaluation.

##### Integer Expressions

| Expression            | Is True If...                                  |
|-----------------------|------------------------------------------------|
| integer1 -eq integer2 | integer1 is equal to integer2.                 |
| integer1 -ne integer2 | integer1 is not equal to integer2.             |
| integer1 -le integer2 | integer1 is less than or equal to integer2.    |
| integer1 -lt integer2 | integer1 is less than integer2.                |
| integer1 -ge integer2 | integer1 is greater than or equal to integer2. |
| integer1 -gt integer2 | integer1 is greater than integer2.             |

The script `test-integer` demonstrates integer evaluation.

`[[ expression ]]` adds regular expressions to `test`.<br>
`string1 =~ regex`

The script `test-integer` fails if INT does not contain an integer.<br>
The script `test-integer2` uses `[[ ]]` to fix the problem.

`[[ ]]` also add pattern matching to the `==` operator. Makes `[[ ]]` useful for evaluating file and pathnames.<br>
`if [[ $FILE == foo.* ]]; then`

##### (( )) - Designed for Integers

`(( ))` command is used for operating on integers.

The script `test-integer2a` uses `(( ))` to simplify script `test-integer2`.

`[[ ]]` and `(( ))` support `&&` `||` and `!` logical operators.<br>
`test` supports `-a` `-o` and `!` logical operators.

### 28 - Reading Keyboard Input

#### read - Read Values from Standard Input

`read` command reads a single line of standard input.<br>
`read [-options] [variable...]`

`read` can assign input to multiple values.<br>
The script `read-multiple` shows how.

##### IFS

The shell variable `IFS` can be used to change the default word separator used by `read`.<br>
The script `read-ifs` changes the separator to `:` to read from `/etc/passwd`.

The shell allows variable assignments immediately before a command.<br>
The assignment alters the environment only for that single command.<br>
The line that starts with `IFS=":"` does this.<br>
The `<<<` operator on the same line is a `here string`. It takes the line of data from the `/etc/passwd` file and feeds it into the standard input of the `read` command.

#### Validating Input

The script `read-validate` shows examples of input validation.

#### Menus

The script `read-menu` shows an example of a menu-driven program.

The script `read-integer` uses the `test` command and a `here string` instead of<br>
the `[[ ]]` command.

### 29 - Flow Control: Looping with while / until

The script `while-menu` uses a `while` loop to improve `read-menu`.

The `until` command is the opposite of `while`, it continues until it receives a zero exit status.

##### Reading Files with Loops

`while` and `until` can process standard input.<br>
The script `while-read` demonstrates.<br>
The script `while-read2` uses while with piped input.

### 31 - Flow Control: Branching with `case`

The script `case-menu` shows the syntax of `case`.

##### Patterns

The patterns used by `case` are the same as used by pathname expansion.

The script `case-patterns` shows examples.

### 32 - Positional Parameters

Use `$0`-`$9` to access command line/function parameters.<br>
Use `$#` to access the number of arguments.

##### `shift` - Getting Access to Many Arguments

The script `posit-param2` shows how to use the `shift` command to sequentially move arguments down.<br>
Try it with a large amount of arguments. Something like `posit-param2 $(ls /usr/bin)`.

##### Simple Applications

The script `file-info` uses positional parameters and `basename` to dynamically update the name of the script.

##### Using Positional Parameters in Shell Functions

Positional parameters work the same in shell functions. Bash functions automatically update the variable `FUNCNAME` to keep track of the currently executed shell function.

#### Handling Positional Parameters en Masse

`*` and `@` Special Parameters

The script `posit-params3` demonstrates how to use these special parameters.

#### A More Complete Application

Added positional parameters, interactivity and the option to output to a file in the `sys_info_page` script.

##### Further Reading
http://wiki.bash-hackers.org/scripting/posparams

### 33 - Flow Control: Looping with `for`

#### `for`: Traditional Shell Form

```
for variable [ in words ]; do
    commands
done
```

`for i in A B C D; do echo $i; done`<br>
`for i in {A..D}; do echo $i; done`<br>
`for i in distros*.txt; do echo "$i"; done`

#### `for`: C Language Form

```
for (( i=0; i<5; i=i+1 )); do
    echo $i
done
```

The `longest-word` script uses a for loop to find the longest string in a file.

If the optional `in` portion of `for` is omitted, `for` defaults to processing positional params.<br>
The `longest-word2` script eliminates the `while` loop in favor of `for`.

##### Further Reading
http://tldp.org/LDP/abs/html/loops1.html

### 34 - Strings and Numbers

#### Parameter Expansion

##### Basic Parameters

`$a` or `${a}` are equivalent, but the braces are required if the parameter is adjacent to other text. Ex. `${a}_file`

##### Expansions to Manage Empty Variables

`${parameter:-word}` if `parameter` is unset or empty, this results in the value `word`.<br>
`${parameter:=word}` if `parameter` is unset or empty, this results in the value `word` and sets `parameter` to the value of `word`.<br>
`${parameter:?word}` if `parameter` is unset or empty, this causes the script to exit with an error and the contents of `word` are sent to standard error.<br>
`${parameter:+word}` if `parameter` is unset or empty, the expansion results in nothing, If `parameter` isn't empty, the value of `word` is substituted for `parameter` but the value of `parameter` is not changed.

##### Expansions That Return Variable Names

`${!prefix*}`
`${!prefix@}`<br>
Both return the names of all variables beginning with `prefix`.

##### String Operations

`${#parameter}` expands into the length of the string contained in `parameter`.

`${#parameter:offset}` expands to the string starting from index `offset`.<br>
`${#parameter:offset:length}` expands to the string from index `offset` for `length` characters.

`${#parameter#pattern}`
`${#parameter##pattern}`<br>
These both remove `pattern` from the leading part of string `parameter`. `pattern` is a wildcard. `#` removes the shortest match, `##` removes the longest.
```
foo=file.txt.zip
echo ${foo#*.}
> txt.zip
echo ${foo##*.}
> zip
```
