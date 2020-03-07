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
`x=5`
`if [ “$x” -eq 5 ]; then echo "equals 5"; else echo "does not equal 5"; fi`

#### Exit Status

`$?` parameter holds the exit status of the last command.
`0` always means success. Any other number `1-255` means failure.
`true` command always executes successfully.
`false` command always executes unsuccessfully.

The `if` statement really only evaluates the exit status of commands.
`if true; then echo "It's true."; fi`

#### test

The `test` command performs checks and comparisons.
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

`[[ expression ]]` adds regular expressions to `test`.
`string1 =~ regex`

The script `test-integer` fails if INT does not contain an integer.
The script `test-integer2` uses `[[ ]]` to fix the problem.

`[[ ]]` also add pattern matching to the `==` operator. Makes `[[ ]]` useful for evaluating file and pathnames.
`if [[ $FILE == foo.* ]]; then`

##### (( )) - Designed for Integers

`(( ))` command is used for operating on integers.

The script `test-integer2a` uses `(( ))` to simplify script `test-integer2`.

`[[ ]]` and `(( ))` support `&&` `||` and `!` logical operators.
`test` supports `-a` `-o` and `!` logical operators.

### 28 - Reading Keyboard Input

#### read - Read Values from Standard Input

`read` command reads a single line of standard input.
`read [-options] [variable...]


