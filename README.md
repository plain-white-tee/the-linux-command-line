# Notes and files for [The Linux Command Line](http://linuxcommand.org/tlcl.php)

***

## Part 4 - Writing Shell Scripts

### 26 - Top-Down Design

#### Shell Functions

    name () {
        commands
        return
    }

#### Local Variables
defined with the `local` keyword.

    funct_1 () {
        local foo # variable foo local to funct_1
        
        foo=1
    }
    
##### Shell Functions in `.bashrc`

Shell functions are preferred over aliases.
You can add this to `.bashrc` to report disk space.

    ds () {
        echo "Disk Space Utilization For $HOSTNAME"
        df -h
    }

### 27 – Flow Control: Branching with if

    x=5
    if [ "$x" -eq 5 ]; then
        echo "x equals 5."
    else
        echo "x does not equal 5."
    fi

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

Table 27-1 lists expressions for evaluating files.
The script `evaluate_status` demonstrates `test`.

##### String Expressions

Table 27-2 lists expressions for evaluating strings.
The script `evaluate_string` demonstrates string evaluation.

##### Integer Expressions

Table 27-3 lists expressions for evaluating integers.

