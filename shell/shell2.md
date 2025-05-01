# Shell Scripting Cheatsheet

A comprehensive guide for shell scripting in Linux environments.

## Table of Contents
- [Shell Scripting Cheatsheet](#shell-scripting-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Shell Types](#shell-types)
  - [Getting Started](#getting-started)
    - [Creating and Running Scripts](#creating-and-running-scripts)
  - [Basic Commands](#basic-commands)
  - [Variables](#variables)
  - [Command Line Arguments](#command-line-arguments)
  - [Input/Output](#inputoutput)
  - [Operators](#operators)
  - [Conditional Statements](#conditional-statements)
  - [Loops](#loops)
  - [Functions](#functions)
  - [Arrays](#arrays)
  - [String Operations](#string-operations)
  - [File Operations](#file-operations)
  - [Process Management](#process-management)
  - [Error Handling](#error-handling)
  - [Makefiles](#makefiles)
  - [Best Practices](#best-practices)

## Shell Types

Shell is the command interpreter in Linux systems. Different types of shells:

- **Bourne Shell (sh)**: Original Unix shell, located at `/bin/sh`
- **Bourne Again Shell (bash)**: Most common shell, enhanced version of sh, at `/bin/bash`
- **C Shell (csh)**: C-like syntax, at `/bin/csh`
- **Korn Shell (ksh)**: Combines features from sh and csh, at `/bin/ksh`
- **Z Shell (zsh)**: Extended bash with improvements, at `/bin/zsh`
- **Fish Shell**: User-friendly shell with autocomplete, at `/usr/bin/fish`

Linux system structure:
- **K**: Kernel (core of the OS)
- **S**: Shell (command interpreter)
- **A**: Applications (user programs)

## Getting Started

### Creating and Running Scripts

1. Create a file with `.sh` extension:
```bash
touch myscript.sh
```

2. Open with a text editor:
```bash
vim myscript.sh
```
   - Press `i` to enter insert mode
   - Type your code
   - Press `Esc` to exit insert mode
   - Type `:wq` to write and quit (or `:qa` to quit without saving)

3. Always start your script with a shebang line:
```bash
#!/bin/bash
```

4. Make the script executable:
```bash
chmod +x myscript.sh
```

5. Run the script:
```bash
./myscript.sh
# or
bash myscript.sh
```

## Basic Commands

```bash
# File and Directory Operations
ls         # List files and directories
cd         # Change directory
pwd        # Print working directory
mkdir      # Create directory
touch      # Create empty file
rm         # Remove files
rmdir      # Remove empty directories
cp         # Copy files
mv         # Move files

# Display File Contents
cat        # Display file contents
less       # Page through file
head       # Display first lines
tail       # Display last lines
grep       # Search for patterns

# System Information
uname -a   # Kernel information
cat /etc/passwd    # List all users
whoami     # Current user
date       # Display date and time
df -h      # Disk usage
free -m    # Memory usage
top        # Process activity
ps         # Process status
```

## Variables

```bash
# Variable Assignment (no spaces around =)
name="John"
age=25

# Accessing Variables
echo $name
echo ${name}  # Recommended for clarity

# Constants (by convention, use uppercase)
readonly PI=3.14

# Special Variables
$0   # Script name
$1-9 # First 9 command line arguments
$#   # Number of arguments
$*   # All arguments as a single string
$@   # All arguments as separate strings
$?   # Exit status of last command (0 = success)
$$   # Process ID of current shell
$!   # Process ID of last background command

# Command substitution
current_date=$(date)
echo "Today is $current_date"

# Arithmetic operations
result=$((5 + 3))
```

## Command Line Arguments

```bash
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "Total arguments: $#"
echo "All arguments: $@"

# Looping through arguments
for arg in "$@"; do
  echo "Argument: $arg"
done
```

## Input/Output

```bash
# User Input
echo "Enter your name:"
read name
echo "Hello $name"

# Reading multiple values
read -p "Enter first and last name: " first last
echo "First: $first, Last: $last"

# Output redirection
echo "Hello World" > output.txt  # Overwrite
echo "More text" >> output.txt   # Append
ls -la 2> error.log              # Redirect stderr
command > output.txt 2>&1        # Redirect both stdout and stderr

# Piping
ls -l | grep ".txt"              # Pipe output to another command
```

## Operators

```bash
# Arithmetic Operators
a=10
b=3
echo $(( a + b ))  # Addition: 13
echo $(( a - b ))  # Subtraction: 7
echo $(( a * b ))  # Multiplication: 30
echo $(( a / b ))  # Division: 3
echo $(( a % b ))  # Modulus: 1
((a++))            # Increment: a = 11
((b--))            # Decrement: b = 2

# Comparison Operators (for numbers in [[ ]])
[[ $a -eq $b ]]    # Equal
[[ $a -ne $b ]]    # Not equal
[[ $a -gt $b ]]    # Greater than
[[ $a -lt $b ]]    # Less than
[[ $a -ge $b ]]    # Greater than or equal
[[ $a -le $b ]]    # Less than or equal

# String Operators
[[ -z $str ]]      # True if string is empty
[[ -n $str ]]      # True if string is not empty
[[ $str1 == $str2 ]] # True if strings are equal
[[ $str1 != $str2 ]] # True if strings are not equal

# File Test Operators
[[ -e $file ]]     # True if file exists
[[ -f $file ]]     # True if file exists and is a regular file
[[ -d $file ]]     # True if file exists and is a directory
[[ -r $file ]]     # True if file exists and is readable
[[ -w $file ]]     # True if file exists and is writable
[[ -x $file ]]     # True if file exists and is executable
[[ -s $file ]]     # True if file exists and is not empty

# Logical Operators
[[ condition1 && condition2 ]]  # AND
[[ condition1 || condition2 ]]  # OR
[[ ! condition ]]               # NOT
```

## Conditional Statements

```bash
# If Statement
if [[ condition ]]; then
    command1
    command2
elif [[ condition2 ]]; then
    command3
else
    command4
fi

# Example
if [[ $age -ge 18 ]]; then
    echo "Adult"
else
    echo "Minor"
fi

# Case Statement
case $variable in
    pattern1)
        commands
        ;;
    pattern2)
        commands
        ;;
    *)  # Default case
        commands
        ;;
esac

# Example
case $fruit in
    "apple")
        echo "Red fruit"
        ;;
    "banana")
        echo "Yellow fruit"
        ;;
    *)
        echo "Unknown fruit"
        ;;
esac
```

## Loops

```bash
# For Loop
for variable in value1 value2 value3; do
    commands
done

# Example
for name in John Sara Tom; do
    echo "Hello $name"
done

# For Loop with sequence
for i in {1..5}; do
    echo "Number $i"
done

# C-style For Loop
for ((i=0; i<5; i++)); do
    echo "Count: $i"
done

# While Loop
while [[ condition ]]; do
    commands
done

# Example
count=0
while [[ $count -lt 5 ]]; do
    echo "Count: $count"
    ((count++))
done

# Until Loop (runs until condition becomes true)
until [[ condition ]]; do
    commands
done

# Break and Continue
for i in {1..10}; do
    if [[ $i -eq 5 ]]; then
        break       # Exit the loop
    fi
    if [[ $i -eq 3 ]]; then
        continue    # Skip to next iteration
    fi
    echo "Number: $i"
done
```

## Functions

```bash
# Function Declaration
function_name() {
    commands
    return value
}

# Function with parameters
greet() {
    echo "Hello, $1!"
}

# Calling the function
greet "John"  # Output: Hello, John!

# Return values
get_sum() {
    local total=$(($1 + $2))  # 'local' keyword makes variable scope limited to function
    return $total
}

get_sum 5 3
echo "Sum: $?"  # $? contains the return value of the last command

# Functions with local variables
calculate() {
    local result=$(($1 * $2))  # Local variable only accessible within the function
    echo $result               # Echo the result (can be captured with command substitution)
}

product=$(calculate 5 4)
echo "Product: $product"
```

## Arrays

```bash
# Declaring Arrays
fruits=("apple" "banana" "orange")
numbers=(1 2 3 4 5)

# Accessing Array Elements
echo ${fruits[0]}     # First element (apple)
echo ${numbers[2]}    # Third element (3)

# Getting All Elements
echo ${fruits[@]}     # All elements
echo ${#fruits[@]}    # Number of elements

# Adding Elements
fruits+=("grape")     # Append element
fruits[4]="mango"     # Add at specific index

# Looping Through Arrays
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

# Slicing Arrays
echo ${fruits[@]:1:2}  # Start at index 1, get 2 elements
```

## String Operations

```bash
# String Length
str="Hello World"
echo ${#str}  # Output: 11

# Substring Extraction
echo ${str:0:5}  # Output: Hello (from position 0, length 5)
echo ${str:6}    # Output: World (from position 6 to end)

# String Replacement
echo ${str/World/Universe}  # Replace first occurrence
echo ${str//l/L}            # Replace all occurrences

# Case Conversion
echo ${str^^}  # To uppercase: HELLO WORLD
echo ${str,,}  # To lowercase: hello world

# String Comparison
if [[ "$str1" == "$str2" ]]; then
    echo "Strings are equal"
fi

# Check if String Contains Substring
if [[ $str == *"Hello"* ]]; then
    echo "String contains Hello"
fi

# Check Beginning/End of String
if [[ $str == "Hello"* ]]; then
    echo "String starts with Hello"
fi

if [[ $str == *"World" ]]; then
    echo "String ends with World"
fi
```

## File Operations

```bash
# Reading a File Line by Line
while IFS= read -r line; do
    echo "Line: $line"
done < input.txt

# Reading a File into an Array
mapfile -t lines < input.txt
# OR
IFS=$'\n' read -d '' -ra lines < input.txt

# Writing to a File
echo "Hello World" > output.txt
echo "Another line" >> output.txt

# Processing CSV
while IFS=, read -r col1 col2 col3; do
    echo "Column 1: $col1, Column 2: $col2, Column 3: $col3"
done < data.csv

# Check if File Exists
if [[ -f "file.txt" ]]; then
    echo "File exists"
fi

# Compare Files
if cmp -s file1.txt file2.txt; then
    echo "Files are identical"
fi
```

## Process Management

```bash
# Run in Background
command &

# Check Running Processes
ps aux | grep "process_name"

# Kill Process
kill PID
kill -9 PID  # Force kill

# Wait for Background Processes
wait

# Execute Command with Timeout
timeout 5s command  # Run command with 5 second timeout

# Run Multiple Commands
command1 && command2  # Run command2 only if command1 succeeds
command1 || command2  # Run command2 only if command1 fails
command1 ; command2   # Run command2 regardless of command1's result
```

## Error Handling

```bash
# Exit on Error
set -e  # Script will exit if any command fails

# Trap Errors
trap 'echo "Error at line $LINENO"; exit 1' ERR

# Custom Error Function
error_exit() {
    echo "$1" >&2
    exit 1
}

# Usage
if [[ ! -f $file ]]; then
    error_exit "File not found: $file"
fi

# Ignore Errors for Specific Command
command || true

# Capture Both stdout and stderr
output=$(command 2>&1)
```

## Makefiles

Makefiles are used to automate build processes and can be integrated with shell scripts.

```makefile
# Basic Makefile syntax
target: dependencies
    commands

# Example
all: build test

build:
    echo "Building..."
    gcc -o myapp main.c

test:
    echo "Testing..."
    ./myapp --test

clean:
    rm -f myapp *.o
```

To use a Makefile:
```bash
make        # Run default target
make build  # Run specific target
make clean  # Clean build artifacts
```

## Best Practices

1. **Always use shebang line**:
   ```bash
   #!/bin/bash
   ```

2. **Use meaningful variable names**:
   ```bash
   user_name="John"  # Good
   un="John"         # Bad
   ```

3. **Quote variables to handle spaces and special characters**:
   ```bash
   file_path="/path/with spaces/file.txt"
   if [[ -f "$file_path" ]]; then  # Quote the variable
       echo "File exists"
   fi
   ```

4. **Use functions for repeated code**:
   ```bash
   log_message() {
       echo "[$(date)] $1"
   }
   log_message "Starting process"
   ```

5. **Comment your code**:
   ```bash
   # This function calculates the factorial of a number
   factorial() {
       # Code here
   }
   ```

6. **Use exit codes properly**:
   ```bash
   if some_command; then
       exit 0  # Success
   else
       exit 1  # Failure
   fi
   ```

7. **Validate input**:
   ```bash
   if [[ -z "$1" ]]; then
       echo "Error: Parameter required"
       exit 1
   fi
   ```

8. **Handle edge cases**:
   ```bash
   file=$1
   if [[ ! -f "$file" ]]; then
       echo "Error: File not found"
       exit 1
   fi
   if [[ ! -r "$file" ]]; then
       echo "Error: File not readable"
       exit 1
   fi
   ```

9. **Use shellcheck to validate scripts**:
   ```bash
   shellcheck myscript.sh
   ```

10. **Use version control** for your scripts (Git, etc.)