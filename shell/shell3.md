# Ultimate Shell Scripting Cheatsheet

A comprehensive guide for shell scripting in Linux environments, from basics to advanced techniques.

## Table of Contents
- [Ultimate Shell Scripting Cheatsheet](#ultimate-shell-scripting-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Shell Fundamentals](#shell-fundamentals)
    - [Shell Types](#shell-types)
    - [Shell Architecture](#shell-architecture)
    - [Environment Setup](#environment-setup)
      - [Shell Configuration Files](#shell-configuration-files)
      - [Path Configuration](#path-configuration)
      - [Shell Aliases](#shell-aliases)
  - [Getting Started](#getting-started)
    - [Creating Scripts](#creating-scripts)
      - [Basic Structure](#basic-structure)
      - [Script File Extensions](#script-file-extensions)
    - [Script Execution](#script-execution)
      - [Making Scripts Executable](#making-scripts-executable)
      - [Different Ways to Run Scripts](#different-ways-to-run-scripts)
      - [Script Execution Environment](#script-execution-environment)
    - [Text Editors](#text-editors)
      - [Common Editors for Shell Scripts](#common-editors-for-shell-scripts)
  - [Basic Commands](#basic-commands)
    - [File and Directory Operations](#file-and-directory-operations)
    - [Display and Text Processing](#display-and-text-processing)
    - [System Information](#system-information)
    - [User Management](#user-management)
    - [Permission Management](#permission-management)
  - [Variables](#variables)
    - [Variable Types](#variable-types)
      - [String Variables](#string-variables)
      - [Integer Variables](#integer-variables)
      - [Readonly Variables](#readonly-variables)
      - [Type Declaration](#type-declaration)
    - [Variable Scope](#variable-scope)
      - [Global Variables](#global-variables)
      - [Local Variables](#local-variables)
    - [Special Variables](#special-variables)
    - [Environment Variables](#environment-variables)
    - [Array Variables](#array-variables)
      - [Indexed Arrays](#indexed-arrays)
      - [Associative Arrays](#associative-arrays)
  - [Command Line Arguments](#command-line-arguments)
    - [Positional Parameters](#positional-parameters)
    - [Argument Parsing](#argument-parsing)
    - [getopts Usage](#getopts-usage)
  - [Input/Output](#inputoutput)
    - [User Input](#user-input)
    - [Output Formatting](#output-formatting)
    - [Redirection](#redirection)
    - [Piping](#piping)
    - [Here Documents](#here-documents)
  - [Operators](#operators)
    - [Arithmetic Operators](#arithmetic-operators)
    - [Comparison Operators](#comparison-operators)
      - [For Numbers](#for-numbers)
    - [String Operators](#string-operators)
    - [File Test Operators](#file-test-operators)
- [File existence and types](#file-existence-and-types)

## Shell Fundamentals

### Shell Types

Shells are command interpreters that provide interfaces to the Linux operating system:

- **Bourne Shell (sh)**: 
  - Original Unix shell created by Stephen Bourne
  - Located at `/bin/sh`
  - Basis for many other shells
  - Simple, efficient, but limited features

- **Bourne Again Shell (bash)**:
  - Most widely used shell in Linux systems
  - Enhanced version of the Bourne Shell
  - Located at `/bin/bash`
  - Feature-rich with command history, command completion, and more
  - Default shell in most Linux distributions

- **C Shell (csh)**:
  - Developed at UC Berkeley
  - Syntax similar to C programming language
  - Located at `/bin/csh`
  - Includes command history and job control

- **TENEX C Shell (tcsh)**:
  - Enhanced version of C Shell
  - Located at `/bin/tcsh`
  - Improved command-line editing and completion

- **Korn Shell (ksh)**:
  - Developed by David Korn at AT&T Bell Labs
  - Combines features from Bourne Shell and C Shell
  - Located at `/bin/ksh`
  - Powerful scripting capabilities

- **Z Shell (zsh)**:
  - Extended Bourne shell with many improvements
  - Located at `/bin/zsh`
  - Powerful completion system, spelling correction, and shared command history

- **Fish Shell**:
  - User-friendly shell focused on interactive use
  - Located at `/usr/bin/fish`
  - Features intuitive auto-suggestions and syntax highlighting

To check your current shell:
```bash
echo $SHELL
```

To change your shell:
```bash
chsh -s /bin/bash username
```

### Shell Architecture

Linux system structure can be understood as layers:

1. **K (Kernel)**: 
   - Core of the operating system
   - Manages system resources (CPU, memory, devices)
   - Provides essential services to applications
   - Handles low-level hardware interactions

2. **S (Shell)**:
   - Command interpreter that interfaces between users and kernel
   - Processes commands and scripts
   - Provides a programming environment
   - Manages input/output redirection

3. **A (Applications)**:
   - User programs and utilities
   - System tools and services
   - Shell scripts themselves are applications

Key shell components:
- **Command processor**: Interprets user commands
- **Scripting engine**: Executes shell scripts
- **Built-in commands**: Commands implemented within the shell
- **External commands**: Programs that the shell can execute

### Environment Setup

#### Shell Configuration Files

For Bash:
- `/etc/profile`: System-wide environment settings
- `~/.bash_profile`: User-specific login settings
- `~/.bashrc`: User-specific shell settings for interactive shells
- `~/.bash_logout`: Commands executed when exiting a login shell

For Zsh:
- `/etc/zshenv`: System-wide environment settings
- `~/.zshenv`: User environment settings
- `~/.zshrc`: User-specific interactive shell settings

#### Path Configuration
The `PATH` environment variable determines where the shell looks for commands:

```bash
# View current PATH
echo $PATH

# Add directory to PATH temporarily
PATH=$PATH:/new/directory

# Add directory to PATH permanently (in ~/.bashrc)
echo 'export PATH=$PATH:/new/directory' >> ~/.bashrc
source ~/.bashrc
```

#### Shell Aliases
Create shortcuts for frequently used commands:

```bash
# Temporary alias
alias ll='ls -la'

# Permanent alias (add to ~/.bashrc)
echo 'alias update="sudo apt update && sudo apt upgrade -y"' >> ~/.bashrc
source ~/.bashrc

# Remove alias
unalias ll
```

## Getting Started

### Creating Scripts

#### Basic Structure
Every shell script should start with a shebang line that specifies the interpreter:

```bash
#!/bin/bash
# This is a comment
echo "Hello, World!"
```

The shebang line (`#!`) tells the system which interpreter to use when executing the script.

#### Script File Extensions
Common extensions for shell scripts:
- `.sh`: Generic shell script
- `.bash`: Specifically for Bash scripts
- `.ksh`: For Korn shell scripts
- `.zsh`: For Z shell scripts

Extensions are not mandatory but help identify script types.

### Script Execution

#### Making Scripts Executable

```bash
# Add execute permission
chmod +x script.sh

# Alternative: add read and execute for user only
chmod u+rx script.sh

# Execute the script
./script.sh
```

#### Different Ways to Run Scripts

```bash
# Method 1: Specify interpreter
bash script.sh

# Method 2: Execute directly (requires execute permission)
./script.sh

# Method 3: Source the script (runs in current shell)
source script.sh
# OR
. script.sh

# Method 4: Run with specific options
bash -x script.sh  # Debug mode
```

#### Script Execution Environment

When a script runs, it creates a new shell instance (subprocess). Variables and settings defined in the parent shell are not automatically available unless:
- They are exported (`export VAR=value`)
- The script is sourced (`. script.sh` or `source script.sh`)

### Text Editors

#### Common Editors for Shell Scripts

**Vim/Vi**:
- Command-based editor
- Available on virtually all UNIX/Linux systems
- Basic operations:
  - `vim script.sh`: Open file
  - `i`: Enter insert mode
  - `Esc`: Exit insert mode
  - `:w`: Save file
  - `:q`: Quit
  - `:wq`: Save and quit
  - `:q!`: Quit without saving

**Nano**:
- Simpler, beginner-friendly
- Menu-driven interface
- Basic operations:
  - `nano script.sh`: Open file
  - `Ctrl+O`: Save file
  - `Ctrl+X`: Exit
  - `Ctrl+K`: Cut line
  - `Ctrl+U`: Paste line

**Emacs**:
- Powerful, extensible editor
- Basic operations:
  - `emacs script.sh`: Open file
  - `Ctrl+x Ctrl+s`: Save file
  - `Ctrl+x Ctrl+c`: Exit

**Visual Studio Code**:
- Modern, graphical editor
- Rich extension ecosystem
- Built-in terminal
- Syntax highlighting for shell scripts

## Basic Commands

### File and Directory Operations

```bash
# Directory Navigation
pwd             # Print working directory
cd directory    # Change to specified directory
cd              # Change to home directory
cd ..           # Move up one directory
cd -            # Return to previous directory

# Directory Listing
ls              # List files and directories
ls -l           # Long format listing
ls -a           # Show hidden files
ls -la          # Combine long format and hidden files
ls -lh          # Human-readable file sizes
ls -R           # Recursive listing
ls -lt          # Sort by modification time
ls -lS          # Sort by size

# Directory Operations
mkdir dir_name                  # Create directory
mkdir -p path/to/nested/dir     # Create nested directories
rmdir dir_name                  # Remove empty directory
rm -r dir_name                  # Remove directory and contents

# File Operations
touch file.txt                  # Create empty file or update timestamp
cp source destination           # Copy file
cp -r source_dir dest_dir       # Copy directory recursively
mv source destination           # Move/rename file or directory
rm file.txt                     # Remove file
rm -f file.txt                  # Force remove without confirmation
ln -s target link_name          # Create symbolic link

# File Compression
tar -czf archive.tar.gz dir/    # Create gzipped tar archive
tar -xzf archive.tar.gz         # Extract gzipped tar archive
gzip file                       # Compress file (creates file.gz)
gunzip file.gz                  # Decompress file.gz
zip -r archive.zip directory    # Create zip archive
unzip archive.zip               # Extract zip archive
```

### Display and Text Processing

```bash
# File Content Display
cat file.txt                    # Display entire file
less file.txt                   # Page through file (q to quit)
more file.txt                   # Simple pager (space to continue)
head file.txt                   # Show first 10 lines
head -n 20 file.txt             # Show first 20 lines
tail file.txt                   # Show last 10 lines
tail -n 20 file.txt             # Show last 20 lines
tail -f file.txt                # Follow file updates in real-time

# Text Searching
grep "pattern" file.txt         # Search for pattern in file
grep -i "pattern" file.txt      # Case-insensitive search
grep -r "pattern" directory     # Recursive search
grep -v "pattern" file.txt      # Show lines NOT matching pattern
grep -n "pattern" file.txt      # Show line numbers with matches
grep -l "pattern" *             # List files containing pattern

# Text Processing
sort file.txt                   # Sort lines alphabetically
sort -n file.txt                # Sort lines numerically
sort -r file.txt                # Sort in reverse order
uniq file.txt                   # Remove adjacent duplicate lines
uniq -c file.txt                # Count occurrences of lines
wc file.txt                     # Count lines, words, characters
wc -l file.txt                  # Count lines only
cut -d':' -f1 file.txt          # Extract first field using ':' delimiter
tr 'a-z' 'A-Z' < file.txt       # Convert lowercase to uppercase

# Text Editing
sed 's/old/new/' file.txt       # Replace first occurrence in each line
sed 's/old/new/g' file.txt      # Replace all occurrences
sed -i 's/old/new/g' file.txt   # Edit file in-place
sed '1d' file.txt               # Delete first line
awk '{print $1}' file.txt       # Print first column
awk -F':' '{print $1}' file.txt # Use ':' as field separator
```

### System Information

```bash
# System and Kernel
uname -a                # All system information
uname -r                # Kernel release
uname -m                # Machine hardware name
cat /etc/os-release     # OS information
lsb_release -a          # Distribution information

# Hardware Information
lscpu                   # CPU information
free -h                 # Memory usage (human-readable)
df -h                   # Disk usage (human-readable)
lsblk                   # Block device information
lspci                   # PCI devices
lsusb                   # USB devices
dmidecode               # DMI/SMBIOS information

# Process Information
ps                      # Current shell processes
ps aux                  # All processes
ps -ef                  # All processes (UNIX style)
top                     # Dynamic process view
htop                    # Enhanced dynamic process view
pgrep process_name      # Find process ID by name
pkill process_name      # Kill process by name

# Network Information
ifconfig                # Network interfaces
ip addr                 # Modern alternative to ifconfig
netstat -tuln           # Listening ports
ss -tuln                # Modern alternative to netstat
ping host               # Check connectivity
traceroute host         # Trace route to host
dig domain              # DNS lookup
host domain             # Simple DNS lookup
```

### User Management

```bash
# User Information
whoami                  # Current username
id                      # User and group IDs
who                     # Users currently logged in
w                       # Who is logged in and what they're doing
last                    # Recent login history
cat /etc/passwd         # All users on system

# User Administration (requires sudo)
useradd username        # Create user
adduser username        # Interactive user creation
usermod -aG group user  # Add user to group
passwd username         # Set user password
su - username           # Switch to user
sudo command            # Execute command as superuser
```

### Permission Management

The permission format is: `rwxrwxrwx` representing:
- First triplet: User/owner permissions
- Second triplet: Group permissions
- Third triplet: Others/world permissions

Where:
- r = 4 (read)
- w = 2 (write)
- x = 1 (execute)

```bash
# View Permissions
ls -l file.txt          # Long listing shows permissions

# Change Permissions
chmod 755 file.txt      # Set to rwxr-xr-x
chmod +x file.txt       # Add execute permission to all
chmod u+w file.txt      # Add write permission for user
chmod g-w file.txt      # Remove write permission from group
chmod o-rwx file.txt    # Remove all permissions for others
chmod -R 755 directory  # Recursively change permissions

# Change Ownership
chown user file.txt     # Change owner
chown user:group file.txt  # Change owner and group
chgrp group file.txt    # Change group only
chown -R user directory # Recursively change ownership
```

## Variables

### Variable Types

#### String Variables
```bash
name="John"                # String assignment
echo $name                 # Access variable value
echo "Hello, $name"        # Variable expansion in double quotes
echo 'Hello, $name'        # No expansion in single quotes
echo "Path is \"$PATH\""   # Escaping special characters
```

#### Integer Variables
```bash
age=30                     # Integer assignment
((age++))                  # Increment
((age--))                  # Decrement
echo $((age * 2))          # Arithmetic expansion
declare -i number=42       # Declare integer type
```

#### Readonly Variables
```bash
readonly PI=3.14159        # Declare constant
declare -r MAX_ATTEMPTS=5  # Alternative syntax
```

#### Type Declaration
```bash
declare -i count=10        # Integer
declare -r timeout=30      # Readonly
declare -l lowercase="TEXT" # Convert to lowercase
declare -u uppercase="text" # Convert to uppercase
declare -a array=(1 2 3)   # Indexed array
declare -A map=([key]=value) # Associative array
```

### Variable Scope

#### Global Variables
Available throughout the script and to child processes if exported:

```bash
global_var="visible everywhere"

# Export to make visible to child processes
export GLOBAL_PATH="/usr/local/bin"
```

#### Local Variables
Limited to function scope:

```bash
function demo() {
    local local_var="only visible in function"
    echo $local_var
    echo $global_var  # Can access global variables
}

demo
echo $local_var      # Error: not defined
```

### Special Variables

```bash
$0          # Script name
$1, $2...   # Positional parameters (arguments)
$#          # Number of arguments
$*          # All arguments as a single string
$@          # All arguments as separate strings
$?          # Exit status of last command (0=success, non-zero=failure)
$$          # Process ID of current shell
$!          # Process ID of last background command
$_          # Last argument of previous command
```

### Environment Variables

Common environment variables:

```bash
echo $HOME        # Home directory
echo $USER        # Current username
echo $HOSTNAME    # Host name
echo $PWD         # Present working directory
echo $SHELL       # Path to current shell
echo $PATH        # Executable search path
echo $LANG        # Current language
echo $RANDOM      # Random number between 0-32767
echo $LINENO      # Current line number in script
echo $SECONDS     # Seconds since script started

# Setting environment variables
export CUSTOM_VAR="value"

# Removing environment variables
unset CUSTOM_VAR
```

### Array Variables

#### Indexed Arrays

```bash
# Declaration and initialization
fruits=("apple" "banana" "orange")
declare -a numbers=(1 2 3 4 5)

# Accessing elements
echo ${fruits[0]}       # First element (apple)
echo ${fruits[-1]}      # Last element (orange)
echo ${fruits[@]}       # All elements
echo ${#fruits[@]}      # Number of elements
echo ${fruits[@]:1:2}   # Slice (banana orange)

# Adding elements
fruits+=("grape")       # Append
fruits[3]="pear"        # Add at specific index

# Removing elements
unset fruits[1]         # Remove element at index 1
```

#### Associative Arrays

```bash
# Declaration (must use declare -A)
declare -A user_info
user_info=([name]="John" [age]=30 [city]="New York")

# Alternative initialization
declare -A colors
colors[red]="#FF0000"
colors[green]="#00FF00"
colors[blue]="#0000FF"

# Accessing elements
echo ${user_info[name]}      # Access by key
echo ${user_info[@]}         # All values
echo ${!user_info[@]}        # All keys
echo ${#user_info[@]}        # Number of elements

# Adding/modifying elements
user_info[email]="john@example.com"

# Removing elements
unset user_info[city]
```

## Command Line Arguments

### Positional Parameters

```bash
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"

# Shifting arguments
shift       # Removes $1, making $2 the new $1
echo "New first argument: $1"

# Accessing arguments beyond 9
echo "Tenth argument: ${10}"
```

### Argument Parsing

Simple argument parsing:

```bash
#!/bin/bash
while [[ $# -gt 0 ]]; do
    case $1 in
        -f|--file)
            file="$2"
            shift 2  # Skip the flag and its value
            ;;
        -v|--verbose)
            verbose=true
            shift    # Skip just the flag
            ;;
        -h|--help)
            echo "Usage: $0 [-f|--file <filename>] [-v|--verbose] [-h|--help]"
            exit 0
            ;;
        *)
            echo "Unknown option: $1"
            exit 1
            ;;
    esac
done
```

### getopts Usage

More structured argument parsing:

```bash
#!/bin/bash
usage() {
    echo "Usage: $0 [-f filename] [-v] [-h]"
    exit 1
}

file=""
verbose=false

while getopts ":f:vh" opt; do
    case $opt in
        f)
            file="$OPTARG"
            ;;
        v)
            verbose=true
            ;;
        h)
            usage
            ;;
        \?)
            echo "Invalid option: -$OPTARG"
            usage
            ;;
        :)
            echo "Option -$OPTARG requires an argument."
            usage
            ;;
    esac
done

# Shift to handle non-option arguments
shift $((OPTIND-1))

# Remaining arguments are in $@
echo "File: $file"
echo "Verbose: $verbose"
echo "Remaining arguments: $@"
```

## Input/Output

### User Input

```bash
# Basic input
echo "Enter your name:"
read name
echo "Hello, $name!"

# Read with prompt
read -p "Enter your age: " age

# Read without echoing (for passwords)
read -sp "Enter password: " password
echo  # New line after password input

# Read with timeout
read -t 5 -p "You have 5 seconds to respond: " response

# Read into array
read -a colors -p "Enter colors (space-separated): "
echo "First color: ${colors[0]}"

# Read with default value
read -p "Enter username [default]: " username
username=${username:-default}
```

### Output Formatting

```bash
# Basic output
echo "Hello World"

# No newline
echo -n "No newline "
echo "after this"

# Interpret backslash escapes
echo -e "Tab\tand\nnew line"

# Color and text formatting using ANSI escape codes
RED='\033[0;31m'
GREEN='\033[0;32m'
BOLD='\033[1m'
NC='\033[0m'  # No Color

echo -e "${RED}Error message${NC}"
echo -e "${GREEN}Success message${NC}"
echo -e "${BOLD}Bold text${NC}"

# printf for formatted output
printf "Name: %-10s Age: %d\n" "John" 30
printf "Pi: %.2f\n" 3.14159

# Formatted table
printf "%-10s %-8s %s\n" "Name" "Age" "City"
printf "%-10s %-8d %s\n" "John" 30 "New York"
printf "%-10s %-8d %s\n" "Alice" 25 "London"
```

### Redirection

```bash
# Output redirection
echo "Hello" > file.txt        # Overwrite file
echo "World" >> file.txt       # Append to file

# Input redirection
sort < file.txt                # Read from file

# Error redirection
command 2> error.log           # Redirect stderr only

# Redirect both stdout and stderr
command > output.log 2>&1      # Traditional syntax
command &> output.log          # Bash shorthand

# Discard output
command > /dev/null
command &> /dev/null           # Discard both stdout and stderr

# Redirect stderr to stdout
command 2>&1 | grep "error"

# Redirect specific file descriptors
# 0: stdin, 1: stdout, 2: stderr
exec 3> custom.log             # Open file descriptor 3
echo "Custom log entry" >&3    # Write to descriptor 3
exec 3>&-                      # Close descriptor 3
```

### Piping

```bash
# Basic piping
ls -l | grep ".txt"            # Filter ls output

# Multiple pipes
cat file.txt | grep "error" | wc -l

# Named pipes (FIFOs)
mkfifo mypipe
ls -l > mypipe &               # Write to pipe in background
grep ".txt" < mypipe           # Read from pipe

# tee command (write to file and stdout)
ls -l | tee listing.txt | grep ".txt"

# Process substitution
diff <(ls dir1) <(ls dir2)     # Compare outputs
```

### Here Documents

```bash
# Basic here-document
cat << EOF
This is a multi-line
text block that will be
passed to cat command.
EOF

# Here-document to file
cat << EOF > config.ini
[settings]
user = $USER
home = $HOME
EOF

# Here-document with indentation preserved
cat << 'EOT'
These lines will be
    exactly as written
  with $variables not expanded
EOT

# Here-document with indentation stripped
cat <<- EOF
	This will ignore
		leading tabs
	but preserve
	  spaces
EOF

# Here-string (simpler alternative for short strings)
grep "pattern" <<< "Text to search in"
```

## Operators

### Arithmetic Operators

```bash
a=10
b=3

# Basic operators
echo $((a + b))  # Addition: 13
echo $((a - b))  # Subtraction: 7
echo $((a * b))  # Multiplication: 30
echo $((a / b))  # Integer division: 3
echo $((a % b))  # Modulus: 1
echo $((a ** b)) # Exponentiation: 1000

# Shorthand operators
((a++))          # Post-increment: a = 11
((++a))          # Pre-increment: a = 12
((a--))          # Post-decrement: a = 11
((--a))          # Pre-decrement: a = 10
((a += b))       # Add and assign: a = 13
((a -= b))       # Subtract and assign: a = 10
((a *= b))       # Multiply and assign: a = 30
((a /= b))       # Divide and assign: a = 10
((a %= b))       # Modulus and assign: a = 1

# Alternative syntax using let
let "c = a + b"
let a++
let "a = b * 3"

# Float arithmetic (using bc)
echo "scale=2; 10/3" | bc  # 3.33
```

### Comparison Operators

#### For Numbers

```bash
# Within double brackets [[ ]]
[[ $a -eq $b ]]  # Equal to
[[ $a -ne $b ]]  # Not equal to
[[ $a -gt $b ]]  # Greater than
[[ $a -lt $b ]]  # Less than
[[ $a -ge $b ]]  # Greater than or equal to
[[ $a -le $b ]]  # Less than or equal to

# Within arithmetic expression (( ))
((a == b))       # Equal to
((a != b))       # Not equal to
((a > b))        # Greater than
((a < b))        # Less than
((a >= b))       # Greater than or equal to
((a <= b))       # Less than or equal to
```

### String Operators

```bash
str1="hello"
str2="world"

# String comparisons
[[ $str1 = $str2 ]]    # Equal (single = works in [[ ]])
[[ $str1 == $str2 ]]   # Equal (preferred in [[ ]])
[[ $str1 != $str2 ]]   # Not equal
[[ $str1 < $str2 ]]    # Less than (ASCII order)
[[ $str1 > $str2 ]]    # Greater than (ASCII order)
[[ -z $str1 ]]         # True if string is empty
[[ -n $str1 ]]         # True if string is not empty

# String concatenation
result="$str1 $str2"   # "hello world"

# String length
echo ${#str1}          # 5

# Substring extraction
echo ${str1:0:2}       # "he" (from position 0, length 2)
echo ${str1:2}         # "llo" (from position 2 to end)

# String replacement
echo ${str1/l/L}       # "heLlo" (replace first l with L)
echo ${str1//l/L}      # "heLLo" (replace all l with L)
```

### File Test Operators

```bash
file="example.txt"
dir="directory"

# File existence and types
[[ -e $file ]]    # File exists
[[ -f $file ]]    # Regular file exists
[[ -d $dir ]]     # Directory exists
[[ -L $file ]]    # Symbolic link exists
[[ -p $file ]]    # Named pipe exists
[[ -S $file ]]