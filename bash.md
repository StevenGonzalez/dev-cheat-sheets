# Bash Scripting Cheat Sheet

## Table of Contents
- [Script Basics](#script-basics)
- [Variables](#variables)
- [Command Line Arguments](#command-line-arguments)
- [User Input](#user-input)
- [Conditionals](#conditionals)
- [Loops](#loops)
- [Functions](#functions)
- [Arrays](#arrays)
- [String Operations](#string-operations)
- [File Operations](#file-operations)
- [Process Management](#process-management)
- [Error Handling](#error-handling)
- [Common Commands](#common-commands)
- [Best Practices](#best-practices)
- [Debugging](#debugging)

## Script Basics

### Shebang and Script Structure
```bash
#!/bin/bash
# This is a comment

# Script description
# Author: Your Name
# Date: 2024-01-01

set -e  # Exit on error
set -u  # Exit on undefined variable
set -o pipefail  # Exit on pipe failure

echo "Hello, World!"
```

### Making Scripts Executable
```bash
# Make script executable
chmod +x script.sh

# Run script
./script.sh

# Run with bash explicitly
bash script.sh
```

### Script Options
```bash
#!/bin/bash

# Strict mode
set -euo pipefail

# Debug mode (print commands as they execute)
set -x

# Verbose mode (print shell input lines)
set -v
```

## Variables

### Variable Declaration and Usage
```bash
# Variable assignment (no spaces around =)
name="John"
age=30
is_active=true

# Using variables
echo "Name: $name"
echo "Age: ${age}"
echo "Status: $is_active"

# Command substitution
current_date=$(date)
user_count=`who | wc -l`

# Environment variables
export PATH="/usr/local/bin:$PATH"
export MY_VAR="value"
```

### Special Variables
```bash
$0    # Script name
$1, $2, $3...  # Positional parameters
$#    # Number of arguments
$@    # All arguments as separate words
$*    # All arguments as single word
$?    # Exit status of last command
$$    # Process ID of current shell
$!    # Process ID of last background command
```

### Variable Types
```bash
# String variables
name="John Doe"
path="/home/user"

# Integer variables
declare -i number=42
number+=10  # number is now 52

# Array variables
declare -a fruits=("apple" "banana" "orange")

# Associative arrays (Bash 4+)
declare -A colors=([red]="#FF0000" [green]="#00FF00" [blue]="#0000FF")

# Read-only variables
readonly CONFIG_FILE="/etc/myapp.conf"

# Export variables
export DATABASE_URL="postgres://localhost/mydb"
```

## Command Line Arguments

### Processing Arguments
```bash
#!/bin/bash

# Simple argument handling
if [ $# -eq 0 ]; then
    echo "Usage: $0 <filename>"
    exit 1
fi

filename=$1
echo "Processing file: $filename"

# Looping through all arguments
for arg in "$@"; do
    echo "Argument: $arg"
done
```

### Using getopts for Options
```bash
#!/bin/bash

# Default values
verbose=false
output_file="output.txt"

# Parse options
while getopts "vo:h" opt; do
    case $opt in
        v)
            verbose=true
            ;;
        o)
            output_file="$OPTARG"
            ;;
        h)
            echo "Usage: $0 [-v] [-o output_file]"
            exit 0
            ;;
        \?)
            echo "Invalid option: -$OPTARG" >&2
            exit 1
            ;;
    esac
done

# Shift to get non-option arguments
shift $((OPTIND-1))

echo "Verbose: $verbose"
echo "Output file: $output_file"
echo "Remaining arguments: $@"
```

### Advanced Argument Parsing
```bash
#!/bin/bash

while [[ $# -gt 0 ]]; do
    case $1 in
        --verbose|-v)
            VERBOSE=true
            shift
            ;;
        --output|-o)
            OUTPUT_FILE="$2"
            shift 2
            ;;
        --help|-h)
            echo "Usage: $0 [--verbose] [--output FILE]"
            exit 0
            ;;
        *)
            echo "Unknown option: $1"
            exit 1
            ;;
    esac
done
```

## User Input

### Reading Input
```bash
# Simple input
echo "What's your name?"
read name
echo "Hello, $name!"

# Read with prompt
read -p "Enter your age: " age

# Read password (hidden input)
read -s -p "Enter password: " password
echo  # New line after hidden input

# Read with timeout
read -t 10 -p "Enter your choice (10 seconds): " choice

# Read single character
read -n 1 -p "Press any key to continue..."
echo

# Read into array
echo "Enter fruits (press Enter after each, empty line to finish):"
fruits=()
while IFS= read -r line && [ -n "$line" ]; do
    fruits+=("$line")
done
```

### Input Validation
```bash
# Validate numeric input
while true; do
    read -p "Enter a number: " input
    if [[ $input =~ ^[0-9]+$ ]]; then
        echo "Valid number: $input"
        break
    else
        echo "Invalid input. Please enter a number."
    fi
done

# Validate email format
validate_email() {
    if [[ $1 =~ ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$ ]]; then
        return 0
    else
        return 1
    fi
}

read -p "Enter email: " email
if validate_email "$email"; then
    echo "Valid email: $email"
else
    echo "Invalid email format"
fi
```

## Conditionals

### If Statements
```bash
# Basic if statement
if [ "$name" == "John" ]; then
    echo "Hello John!"
fi

# If-else
if [ $age -ge 18 ]; then
    echo "You are an adult"
else
    echo "You are a minor"
fi

# If-elif-else
if [ $score -ge 90 ]; then
    grade="A"
elif [ $score -ge 80 ]; then
    grade="B"
elif [ $score -ge 70 ]; then
    grade="C"
else
    grade="F"
fi
```

### Test Conditions
```bash
# File tests
[ -f file.txt ]     # File exists and is regular file
[ -d directory ]    # Directory exists
[ -r file.txt ]     # File is readable
[ -w file.txt ]     # File is writable
[ -x script.sh ]    # File is executable
[ -s file.txt ]     # File exists and is not empty
[ -L link ]         # File is symbolic link

# String tests
[ -z "$string" ]    # String is empty
[ -n "$string" ]    # String is not empty
[ "$str1" == "$str2" ]  # Strings are equal
[ "$str1" != "$str2" ]  # Strings are not equal
[ "$str1" \< "$str2" ]  # String comparison (lexicographic)

# Numeric tests
[ $num1 -eq $num2 ]  # Equal
[ $num1 -ne $num2 ]  # Not equal
[ $num1 -lt $num2 ]  # Less than
[ $num1 -le $num2 ]  # Less than or equal
[ $num1 -gt $num2 ]  # Greater than
[ $num1 -ge $num2 ]  # Greater than or equal
```

### Modern Test Syntax
```bash
# Double brackets (more features)
if [[ $name == "John" || $name == "Jane" ]]; then
    echo "Hello $name!"
fi

# Pattern matching
if [[ $filename == *.txt ]]; then
    echo "Text file detected"
fi

# Regular expressions
if [[ $email =~ ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$ ]]; then
    echo "Valid email"
fi
```

### Case Statements
```bash
case $choice in
    1)
        echo "Option 1 selected"
        ;;
    2)
        echo "Option 2 selected"
        ;;
    3|4)
        echo "Option 3 or 4 selected"
        ;;
    [5-9])
        echo "Option 5-9 selected"
        ;;
    *)
        echo "Invalid option"
        ;;
esac

# Case with patterns
case $filename in
    *.txt)
        echo "Text file"
        ;;
    *.jpg|*.png|*.gif)
        echo "Image file"
        ;;
    *.sh)
        echo "Shell script"
        ;;
    *)
        echo "Unknown file type"
        ;;
esac
```

## Loops

### For Loops
```bash
# Loop over list
for item in apple banana orange; do
    echo "Fruit: $item"
done

# Loop over array
fruits=("apple" "banana" "orange")
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

# Loop over files
for file in *.txt; do
    echo "Processing $file"
done

# C-style for loop
for ((i=1; i<=10; i++)); do
    echo "Number: $i"
done

# Loop over command output
for user in $(cat /etc/passwd | cut -d: -f1); do
    echo "User: $user"
done
```

### While Loops
```bash
# Basic while loop
counter=1
while [ $counter -le 5 ]; do
    echo "Count: $counter"
    ((counter++))
done

# Reading file line by line
while IFS= read -r line; do
    echo "Line: $line"
done < file.txt

# Infinite loop
while true; do
    echo "Press Ctrl+C to exit"
    sleep 1
done

# While with condition check
while [ ! -f /tmp/ready ]; do
    echo "Waiting for ready file..."
    sleep 2
done
```

### Until Loops
```bash
# Until loop (opposite of while)
counter=1
until [ $counter -gt 5 ]; do
    echo "Count: $counter"
    ((counter++))
done
```

### Loop Control
```bash
for i in {1..10}; do
    if [ $i -eq 3 ]; then
        continue  # Skip iteration
    fi
    if [ $i -eq 8 ]; then
        break     # Exit loop
    fi
    echo "Number: $i"
done
```

## Functions

### Function Definition and Usage
```bash
# Basic function
greet() {
    echo "Hello, $1!"
}

# Call function
greet "World"

# Function with multiple parameters
calculate_sum() {
    local num1=$1
    local num2=$2
    local sum=$((num1 + num2))
    echo $sum
}

result=$(calculate_sum 10 20)
echo "Sum: $result"

# Function with return value
is_even() {
    local number=$1
    if [ $((number % 2)) -eq 0 ]; then
        return 0  # True
    else
        return 1  # False
    fi
}

if is_even 4; then
    echo "4 is even"
fi
```

### Advanced Functions
```bash
# Function with local variables
process_data() {
    local input_file=$1
    local output_file=$2
    local temp_file="/tmp/processing_$$"
    
    # Process data
    cat "$input_file" | sort > "$temp_file"
    mv "$temp_file" "$output_file"
    
    echo "Processing complete"
}

# Function with default parameters
greet_with_default() {
    local name=${1:-"World"}
    local greeting=${2:-"Hello"}
    echo "$greeting, $name!"
}

greet_with_default              # Hello, World!
greet_with_default "John"       # Hello, John!
greet_with_default "Jane" "Hi"  # Hi, Jane!

# Function that modifies global variables
increment_counter() {
    ((global_counter++))
}

global_counter=0
increment_counter
echo "Counter: $global_counter"  # Counter: 1
```

## Arrays

### Indexed Arrays
```bash
# Array declaration
fruits=("apple" "banana" "orange")
numbers=(1 2 3 4 5)

# Access elements
echo ${fruits[0]}        # First element
echo ${fruits[@]}        # All elements
echo ${fruits[*]}        # All elements (different quoting behavior)
echo ${#fruits[@]}       # Array length

# Add elements
fruits+=("grape")
fruits[10]="mango"       # Sparse array

# Loop through array
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done

# Loop with indices
for i in "${!fruits[@]}"; do
    echo "Index $i: ${fruits[i]}"
done
```

### Associative Arrays
```bash
# Declare associative array (Bash 4+)
declare -A person
person[name]="John"
person[age]=30
person[city]="New York"

# Access elements
echo "Name: ${person[name]}"
echo "Age: ${person[age]}"

# Get all keys
for key in "${!person[@]}"; do
    echo "$key: ${person[key]}"
done

# Get all values
for value in "${person[@]}"; do
    echo "Value: $value"
done
```

### Array Operations
```bash
# Array slicing
numbers=(1 2 3 4 5 6 7 8 9 10)
echo ${numbers[@]:2:3}    # Elements 2,3,4 (3 elements starting from index 2)
echo ${numbers[@]:5}      # Elements from index 5 to end

# Array manipulation
original=("a" "b" "c" "d")
reversed=($(printf '%s\n' "${original[@]}" | tac))
sorted=($(printf '%s\n' "${original[@]}" | sort))

# Remove elements
unset original[1]         # Remove element at index 1
original=("${original[@]}")  # Reindex array
```

## String Operations

### String Manipulation
```bash
string="Hello World"

# String length
echo ${#string}           # 11

# Substring extraction
echo ${string:0:5}        # "Hello"
echo ${string:6}          # "World"
echo ${string: -5}        # "World" (space before -)

# Find and replace
echo ${string/o/O}        # "HellO World" (first occurrence)
echo ${string//o/O}       # "HellO WOrld" (all occurrences)
echo ${string/World/Universe}  # "Hello Universe"

# Remove pattern
filename="document.pdf"
echo ${filename%.pdf}     # "document" (remove .pdf from end)
echo ${filename%.*}       # "document" (remove extension)

path="/home/user/file.txt"
echo ${path##*/}          # "file.txt" (remove path, keep filename)
echo ${path%/*}           # "/home/user" (remove filename, keep path)
```

### String Comparison and Testing
```bash
string1="hello"
string2="world"

# Case conversion
echo ${string1^}          # "Hello" (capitalize first letter)
echo ${string1^^}         # "HELLO" (uppercase)
echo ${string2,}          # "world" (lowercase first letter)
echo ${string2,,}         # "world" (lowercase all)

# Default values
echo ${undefined_var:-"default"}      # "default" if undefined_var is unset
echo ${undefined_var:="default"}      # Set and return default if unset
echo ${defined_var:+"alternative"}    # "alternative" if defined_var is set
```

### Advanced String Operations
```bash
# String contains substring
if [[ "$string" == *"World"* ]]; then
    echo "Contains 'World'"
fi

# String starts with
if [[ "$string" == "Hello"* ]]; then
    echo "Starts with 'Hello'"
fi

# String ends with
if [[ "$string" == *"World" ]]; then
    echo "Ends with 'World'"
fi

# Split string into array
IFS=',' read -ra parts <<< "apple,banana,orange"
for part in "${parts[@]}"; do
    echo "Part: $part"
done
```

## File Operations

### File Testing and Information
```bash
file="example.txt"

# File tests
if [ -f "$file" ]; then
    echo "File exists"
fi

if [ -r "$file" ]; then
    echo "File is readable"
fi

# File information
stat "$file"
ls -la "$file"
file "$file"              # File type
wc -l "$file"            # Line count
```

### Reading Files
```bash
# Read entire file
content=$(cat file.txt)

# Read file line by line
while IFS= read -r line; do
    echo "Line: $line"
done < file.txt

# Read file into array
mapfile -t lines < file.txt
# or
readarray -t lines < file.txt

# Read first N lines
head -n 10 file.txt

# Read last N lines
tail -n 10 file.txt

# Follow file changes
tail -f log.txt
```

### Writing Files
```bash
# Write to file (overwrite)
echo "Hello World" > output.txt

# Append to file
echo "Another line" >> output.txt

# Write multiple lines
cat > output.txt << EOF
Line 1
Line 2
Line 3
EOF

# Write with variables
cat > config.txt << EOF
database_host=$DB_HOST
database_port=$DB_PORT
database_name=$DB_NAME
EOF
```

### File Operations
```bash
# Copy files
cp source.txt destination.txt
cp -r source_dir/ destination_dir/

# Move/rename files
mv old_name.txt new_name.txt
mv file.txt /new/location/

# Delete files
rm file.txt
rm -rf directory/

# Create directories
mkdir new_directory
mkdir -p path/to/nested/directory

# Find files
find . -name "*.txt"
find . -type f -mtime -7    # Files modified in last 7 days
find . -size +1M            # Files larger than 1MB
```

### File Permissions
```bash
# Change permissions
chmod 755 script.sh         # rwxr-xr-x
chmod +x script.sh          # Add execute permission
chmod -w file.txt           # Remove write permission

# Change ownership
chown user:group file.txt
chgrp group file.txt

# Check permissions
ls -la file.txt
stat -c "%A %U %G" file.txt
```

## Process Management

### Running Commands
```bash
# Run command in background
long_running_command &
background_pid=$!

# Wait for background process
wait $background_pid

# Run multiple commands
command1 && command2        # Run command2 only if command1 succeeds
command1 || command2        # Run command2 only if command1 fails
command1; command2          # Run both commands regardless

# Pipe commands
cat file.txt | grep "pattern" | sort | uniq
```

### Process Information
```bash
# Current process ID
echo $$

# Last background process ID
echo $!

# Process status
ps aux
ps -ef

# Find processes
pgrep -f "process_name"
pidof process_name

# Kill processes
kill $pid
kill -9 $pid               # Force kill
killall process_name
pkill -f "pattern"
```

### Job Control
```bash
# List jobs
jobs

# Bring job to foreground
fg %1

# Send job to background
bg %1

# Disown job (continue after shell exit)
disown %1

# nohup (no hangup)
nohup long_running_command &
```

## Error Handling

### Exit Codes
```bash
# Check exit code of last command
if [ $? -eq 0 ]; then
    echo "Command succeeded"
else
    echo "Command failed"
fi

# Set exit code
exit 0    # Success
exit 1    # General error
exit 2    # Specific error
```

### Error Handling Patterns
```bash
# Simple error handling
command || {
    echo "Command failed!"
    exit 1
}

# Function with error handling
safe_command() {
    local cmd="$1"
    if ! $cmd; then
        echo "Error: $cmd failed" >&2
        return 1
    fi
}

# Trap errors
trap 'echo "Error on line $LINENO"' ERR

# Cleanup on exit
cleanup() {
    echo "Cleaning up..."
    rm -f /tmp/temp_file_$$
}
trap cleanup EXIT

# Handle interrupts
interrupt_handler() {
    echo "Script interrupted!"
    cleanup
    exit 130
}
trap interrupt_handler INT TERM
```

### Logging
```bash
# Redirect output
command > output.log 2>&1   # Redirect stdout and stderr
command 2>/dev/null         # Suppress errors
command >/dev/null 2>&1     # Suppress all output

# Logging function
log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1" | tee -a script.log
}

log "Script started"
log "Processing data..."
log "Script completed"
```

## Common Commands

### Text Processing
```bash
# grep - search text
grep "pattern" file.txt
grep -r "pattern" directory/
grep -i "pattern" file.txt     # Case-insensitive
grep -v "pattern" file.txt     # Invert match
grep -n "pattern" file.txt     # Show line numbers

# sed - stream editor
sed 's/old/new/g' file.txt     # Replace all occurrences
sed -i 's/old/new/g' file.txt  # Edit file in-place
sed -n '10,20p' file.txt       # Print lines 10-20

# awk - text processing
awk '{print $1}' file.txt      # Print first column
awk -F',' '{print $2}' file.csv  # CSV processing
awk 'NR==2' file.txt           # Print second line
awk '/pattern/ {print $0}' file.txt  # Print matching lines

# sort and uniq
sort file.txt
sort -n numbers.txt            # Numeric sort
sort -k2 file.txt             # Sort by second column
uniq file.txt                 # Remove duplicates
sort file.txt | uniq -c       # Count occurrences

# cut - extract columns
cut -d',' -f1,3 file.csv      # Extract columns 1 and 3
cut -c1-10 file.txt           # Extract characters 1-10
```

### System Information
```bash
# System info
uname -a                      # System information
whoami                        # Current user
id                           # User and group IDs
hostname                     # System hostname
uptime                       # System uptime

# Disk usage
df -h                        # Disk usage
du -sh directory/            # Directory size
du -h --max-depth=1         # Size of subdirectories

# Memory and CPU
free -h                      # Memory usage
top                         # Process monitor
htop                        # Enhanced process monitor
```

### Network Commands
```bash
# Network info
ifconfig                     # Network interfaces (deprecated)
ip addr show                 # Network interfaces (modern)
netstat -tuln               # Network connections
ss -tuln                    # Socket statistics (modern)

# Connectivity
ping google.com
wget https://example.com/file.txt
curl -s https://api.github.com/users/octocat
```

## Best Practices

### Script Header Template
```bash
#!/bin/bash

###########################################
# Script Name: script_name.sh
# Description: Brief description of what the script does
# Author: Your Name
# Date: 2024-01-01
# Version: 1.0
###########################################

# Exit on any error
set -e

# Exit on undefined variable
set -u

# Exit on pipe failure
set -o pipefail

# Enable debug mode (uncomment for debugging)
# set -x

# Script configuration
readonly SCRIPT_NAME=$(basename "$0")
readonly SCRIPT_DIR=$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)
readonly LOG_FILE="/tmp/${SCRIPT_NAME%.sh}.log"

# Colors for output
readonly RED='\033[0;31m'
readonly GREEN='\033[0;32m'
readonly YELLOW='\033[1;33m'
readonly NC='\033[0m' # No Color

# Logging functions
log_info() {
    echo -e "${GREEN}[INFO]${NC} $1" | tee -a "$LOG_FILE"
}

log_warn() {
    echo -e "${YELLOW}[WARN]${NC} $1" | tee -a "$LOG_FILE"
}

log_error() {
    echo -e "${RED}[ERROR]${NC} $1" | tee -a "$LOG_FILE" >&2
}

# Cleanup function
cleanup() {
    log_info "Cleaning up..."
    # Add cleanup commands here
}

# Error handler
error_handler() {
    log_error "Error occurred in ${BASH_SOURCE[1]}:${BASH_LINENO[0]}. '${BASH_COMMAND}' exited with status $?"
    cleanup
    exit 1
}

# Set up traps
trap cleanup EXIT
trap error_handler ERR

# Main script logic starts here
main() {
    log_info "Starting $SCRIPT_NAME"
    
    # Your script logic here
    
    log_info "$SCRIPT_NAME completed successfully"
}

# Run main function
main "$@"
```

### Security Best Practices
```bash
# Always quote variables
echo "$variable"              # Good
echo $variable               # Bad (word splitting issues)

# Use arrays for multiple values
files=("file1.txt" "file2.txt" "file with spaces.txt")
for file in "${files[@]}"; do
    echo "$file"
done

# Validate input
validate_input() {
    local input="$1"
    if [[ ! $input =~ ^[a-zA-Z0-9_-]+$ ]]; then
        log_error "Invalid input: $input"
        return 1
    fi
}

# Use temporary files safely
temp_file=$(mktemp)
trap "rm -f '$temp_file'" EXIT

# Check if commands exist
if ! command -v git &> /dev/null; then
    log_error "git is not installed"
    exit 1
fi
```

## Debugging

### Debug Techniques
```bash
# Enable debug mode
set -x                       # Print commands as executed
set +x                       # Disable debug mode

# Add debug output
debug() {
    if [[ ${DEBUG:-} == "true" ]]; then
        echo "DEBUG: $*" >&2
    fi
}

DEBUG=true debug "This is a debug message"

# Check variable contents
declare -p variable_name     # Show variable type and value
echo "Variable: '$variable'" # Show with quotes to see spaces

# Function tracing
PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]}: '
set -x
```

### Common Debugging Commands
```bash
# Check script syntax
bash -n script.sh

# Trace script execution
bash -x script.sh

# Check if variable is set
if [[ -v variable_name ]]; then
    echo "Variable is set"
fi

# Show all variables
set | grep "^variable_prefix"
```

---

*Remember: Always test your scripts thoroughly and follow security best practices. Use `shellcheck` to lint your scripts for common issues.*