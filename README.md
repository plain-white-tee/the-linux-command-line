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


