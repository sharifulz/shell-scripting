## Declaring and Using Functions
In shell scripting, functions allow you to group a series of commands together and give them a name, making your code more organized and modular. To declare a function, you use the following syntax:
function_name() {
# Commands to be executed
}
Here's an example of a simple function that prints a greeting:
# Declare a function named greet
greet() {
```bash
echo "Hello, how are you?"
```
}
# Call the greet function
greet
## Function Arguments and Return Values
Shell functions can accept arguments just like command-line scripts. You access these arguments using special variables: $1 for the first argument, $2 for the second, and so on. To access all the arguments, you use $@ or $*.
Here's an example of a function that takes two arguments and prints them:
# Declare a function named print_args
print_args() {
```bash
echo "First argument: $1"
```
```bash
echo "Second argument: $2"
```
}
# Call the print_args function with arguments
print_args "Hello" "World"
Shell functions can't directly return values like functions in some other programming languages. However, you can use the exit status of a function to convey success (0) or failure (non-zero). If you need to pass values back from a function, you can print them and capture the output using command substitution.
Here's an example of a function that calculates the sum of two numbers and returns it through the exit status and output:
# Declare a function named calculate_sum
calculate_sum() {
local num1="$1"
local num2="$2"
local sum=$((num1 + num2))
```bash
echo "$sum"
```
return $sum
}
# Call the calculate_sum function and capture the output
result=$(calculate_sum 10 20)
```bash
echo "Sum: $result"
```
## Scope of Variables
Variables declared within a function have local scope, meaning they're only accessible within that function. To create local variables, use the local keyword. Variables declared outside functions have global scope and can be accessed from anywhere.
Here's an example illustrating local and global variables:
# Declare a global variable
global_var="I'm global"
# Declare a function with local variables
local_variables() {
local local_var="I'm local"
```bash
echo "Inside function: $local_var"
```
```bash
echo "Inside function: $global_var"
```
}
# Call the local_variables function
local_variables
# Access global variable outside the function
```bash
echo "Outside function: $global_var"
```
# Attempting to access local_var here will result in an error
In the example above, the local_var is accessible only within the local_variables function, while global_var is accessible both inside and outside the function.
Remember that each instance of a function call has its own set of local variables, ensuring that they don't interfere with each other.
## String Manipulation in Shell Scripts
String manipulation in shell scripting involves various operations on strings, such as concatenation, substring extraction, searching, and replacing. These operations are commonly used when working with text data in scripts. Let's explore each operation with examples:
1. Concatenation: Concatenation involves combining two or more strings to create a new string. In shell scripting, you can achieve this using variables and the concatenation operator (.).
```bash
#!/bin/bash
```
string1="Hello, "
string2="World!"
result=$string1$string2
```bash
echo "Concatenated string: $result"
```
Output:
Concatenated string: Hello, World!
2. Substring Extraction: You can extract a portion of a string using substrings. In shell scripting, you use parameter expansion to achieve this.
```bash
#!/bin/bash
```
string="Hello, World!"
substring=${string:7:5} # Starting from index 7, extract 5 characters
```bash
echo "Substring: $substring"
```
Output:
Substring: World
3. Searching and Replacing: Searching involves finding a specific substring within a string, and replacing involves substituting one substring with another.
```bash
#!/bin/bash
```
string="Hello, World! Hello!"
search="Hello"
replace="Hi"
result=${string//$search/$replace} # Replace all occurrences
```bash
echo "Original string: $string"
```
```bash
echo "Result after replacement: $result"
```
Output:
Original string: Hello, World! Hello!
Result after replacement: Hi, World! Hi!
You can also use parameter expansion to replace the first occurrence or perform case-insensitive replacements.
Here's a script that combines all three operations:
```bash
#!/bin/bash
```
string1="Hello, "
string2="World!"
concatenated=$string1$string2
original="Hello, World! Hello!"
search="Hello"
replace="Hi"
replaced=${original//$search/$replace}
```bash
echo "Concatenated string: $concatenated"
```
```bash
echo "Original string: $original"
```
```bash
echo "Replaced string: $replaced"
```
substring=${replaced:0:5}
```bash
echo "Extracted substring: $substring"
```
Output:
Concatenated string: Hello, World!
Original string: Hello, World! Hello!
Replaced string: Hi, World! Hi!
Extracted substring: Hi, W
## Arrays
1. Declaring and Using Arrays: In shell scripting, you can declare an array by assigning values to consecutive indices. Arrays in shell scripts are 0-indexed.
Example:
```bash
#!/bin/bash
```
# Declare an array with values
fruits=("Apple" "Banana" "Orange")
# Access array elements
```bash
echo "First fruit: ${fruits[0]}"
```
```bash
echo "Second fruit: ${fruits[1]}"
```
```bash
echo "Third fruit: ${fruits[2]}"
```
Output:
First fruit: Apple
Second fruit: Banana
Third fruit: Orange
2. Looping Through Arrays: You can use loops to iterate through array elements.
Example:
```bash
#!/bin/bash
```
fruits=("Apple" "Banana" "Orange")
# Loop through array using for loop
```bash
echo "Using for loop:"
```
for fruit in "${fruits[@]}"; do
```bash
echo "Fruit: $fruit"
```
done
# Loop through array using while loop and index
```bash
echo "Using while loop:"
```
index=0
while [ $index -lt ${#fruits[@]} ]; do
```bash
echo "Fruit at index $index: ${fruits[$index]}"
```
index=$((index + 1))
done
Output:
Using for loop:
Fruit: Apple
Fruit: Banana
Fruit: Orange
Using while loop:
Fruit at index 0: Apple
Fruit at index 1: Banana
Fruit at index 2: Orange
3. Array Manipulation: You can modify arrays by adding, removing, and updating elements.
Example:
```bash
#!/bin/bash
```
fruits=("Apple" "Banana" "Orange")
# Adding an element
fruits+=("Grapes")
# Updating an element
fruits[1]="Mango"
# Removing an element
unset fruits[0]
# Display the modified array
```bash
echo "Modified array:"
```
for fruit in "${fruits[@]}"; do
```bash
echo "Fruit: $fruit"
```
done
Output:
Modified array:
Fruit: Mango
Fruit: Orange
Fruit: Grapes
Note: Some shell variants, like sh, might not support all these features, especially more advanced array manipulation. For extensive array manipulation, consider using a shell like bash.
## Shell Scripting with Command-Line Arguments
Command-line arguments are values or options provided to a script or program when it's executed. Shell scripts can access these arguments to customize their behavior. Here's how you can work with command-line arguments in shell scripting, along with examples and explanations:
### Accessing Command-Line Arguments
In a shell script, command-line arguments are accessible using special variables:
- $0 represents the script's name itself.
- $1, $2, ... represent the first, second, and so on, arguments.
- $# gives the total number of arguments.
- $@ represents all the arguments as a list.
- $* represents all the arguments as a single string.
Example: Script to Print Command-Line Arguments
```bash
#!/bin/bash
```
```bash
echo "Script name: $0"
```
```bash
echo "First argument: $1"
```
```bash
echo "Second argument: $2"
```
```bash
echo "Total number of arguments: $#"
```
```bash
echo "All arguments as list: $@"
```
```bash
echo "All arguments as string: $*"
```
Executing the Script:
Assuming the script is saved as args_script.sh:
```bash
$ chmod +x args_script.sh
```
```bash
$ ./args_script.sh arg1 arg2 arg3
```
Output:
Script name: ./args_script.sh
First argument: arg1
Second argument: arg2
Total number of arguments: 3
All arguments as list: arg1 arg2 arg3
All arguments as string: arg1 arg2 arg3
Argument Parsing Libraries:
When command-line arguments become complex, using argument parsing libraries can simplify the process of handling arguments, options, and flags. These libraries offer features like long and short option parsing, default values, help messages, and more. Some popular libraries include:
- getopt
- getopts
- argparse (Python-based library usable in shell scripts)
## Error Handling Error handling in shell scripting is crucial to ensure your scripts handle unexpected situations gracefully. This involves dealing with exit codes, error messages, and trapping signals. Let's break down each of these aspects with examples and outputs:
1. Exit Codes: Exit codes are numeric values returned by commands upon completion. Conventionally, an exit code of 0 indicates success, while non-zero values indicate errors.
Example Program (example_exit_codes.sh):
```bash
#!/bin/bash
```
```bash
echo "Starting script..."
```
```bash
ls /nonexistent-directory
```
if [ $? -eq 0 ]; then
```bash
echo "Directory exists."
```
else
```bash
echo "Directory does not exist."
```
fi
```bash
echo "Script finished."
```
Output:
Starting script...
ls: cannot access '/nonexistent-directory': No such file or directory
Directory does not exist.
Script finished.
In this example, the ls command fails to list the contents of a nonexistent directory. The exit code is checked using $?, and the script handles the failure by printing an error message.
2. Error Messages: Custom error messages help users understand what went wrong. You can use echo to print error messages along with relevant information.
Example Program (example_error_messages.sh):
```bash
#!/bin/bash
```
file="nonexistent-file.txt"
if [ ! -f "$file" ]; then
```bash
echo "Error: File '$file' does not exist."
```
exit 1
fi
```bash
echo "File '$file' exists."
```
Output:
Error: File 'nonexistent-file.txt' does not exist.
Here, the script checks for the existence of a file. Since the file doesn't exist, an error message is printed, and the script exits with an exit code of 1.
3. Trap for Handling Signals: The trap command allows you to specify actions to be taken when certain signals are received, like when the script receives Ctrl+C (SIGINT).
Example Program (example_trap.sh):
```bash
#!/bin/bash
```
cleanup() {
```bash
echo "Cleaning up..."
```
# Additional cleanup steps can be added here
exit 1
}
trap cleanup INT
```bash
echo "Running..."
```
sleep 10
Output:
Running...
^CCleaning up...
In this example, the script sets up a cleanup function using the trap command. When the script receives the SIGINT signal (Ctrl+C), the cleanup function is executed, allowing you to perform cleanup actions before exiting.
These examples showcase how to handle errors in shell scripts using exit codes, error messages, and signal trapping. Effective error handling improves the reliability and usability of your scripts, making them more robust in handling unexpected situations.
## Regular Expressions Regular expressions (regex or regexp) are powerful tools for pattern matching and text manipulation. They allow you to define complex patterns to search for and manipulate strings based on certain criteria.
Regular expressions are used in various Unix command-line tools like grep, sed, and awk to perform pattern matching and text transformations.
Let's dive into each tool with examples:
1. grep: grep is a command-line tool used to search for specific patterns in text files.
Example: Searching for a Pattern Suppose you have a file named sample.txt with the following content:
apple
banana
cherry
date
grape
You can use grep to search for lines containing the word "banana":
```bash
grep "banana" sample.txt
```
Output:
banana
2. sed: sed (Stream Editor) is a command-line tool for performing basic text transformations on an input stream.
Example: Replacing a Pattern Suppose you have the same sample.txt file. You can use sed to replace all occurrences of "cherry" with "orange":
```bash
sed 's/cherry/orange/' sample.txt
```
Output:
apple
banana
orange
date
grape
3. awk: awk is a versatile tool for text processing and reporting. It can also handle pattern matching and manipulation.
Example: Extracting Specific Fields Suppose you have a file named data.txt with the following content:
John 25
Alice 30
Bob 28
Eve 22
You can use awk to print only the names of people who are older than 25:
```bash
awk '$2 > 25 { print $1 }' data.txt
```
Output:
Alice
Bob
Using Regular Expressions: Regular expressions add more flexibility and power to these tools.
Example: Using grep with Regular Expression Suppose you have a file named emails.txt with email addresses, and you want to find all Gmail addresses:
```bash
grep "@gmail\.com" emails.txt
```
Output:
john@gmail.com
alice@gmail.com
In this example, the dot (.) is a special character in regex, so we escape it with a backslash (\) to match a literal dot.
Example: Using sed with Regular Expression Suppose you want to replace all occurrences of dates in the format "dd/mm/yyyy" with "mm/dd/yyyy" in a file named dates.txt:
```bash
sed 's/\([0-9]\{2\}\)\/\([0-9]\{2\}\)\/\([0-9]\{4\}\)/\2\/\1\/\3/' dates.txt
```
Example: Using awk with Regular Expression Suppose you have a file named log.txt with lines containing dates and events. You want to print lines with events that contain the word "error":
```bash
awk '/error/ { print }' log.txt
```
## Pipeline and Redirection in Shell Scripts
In shell scripting, pipelines and redirection are powerful concepts that allow you to manipulate input and output streams of commands to achieve more complex and flexible operations.
1. Piping Commands Together:
Piping commands involves sending the output of one command as the input to another command. This is achieved using the | (pipe) operator.
Example 1: List files and directories, and then filter for specific files using grep:
```bash
ls -l | grep ".txt"
```
In this example, the ls -l command lists files and directories in long format, and the output is piped to grep to filter and display only the lines containing ".txt".
Example 2: Count the number of lines in a file using wc:
```bash
cat file.txt | wc -l
```
Here, cat reads the content of the file, and its output is piped to wc -l, which counts the number of lines.
2. Redirecting Input and Output:
Redirection involves changing the source or destination of input or output streams of a command. The operators used for redirection are > (output) and < (input).
Example 1: Redirect Output to a File:
```bash
ls > file_list.txt
```
This redirects the output of the ls command to the file file_list.txt instead of printing it to the terminal.
Example 2: Append Output to a File:
```bash
echo "New content" >> file_list.txt
```
The >> operator appends the output to the end of the file.
Example 3: Redirect Input from a File:
```bash
sort < unsorted.txt > sorted.txt
```
This takes the content of unsorted.txt as input to the sort command and redirects the sorted output to sorted.txt.
Example 4: Combining Redirection and Piping:
```bash
cat file.txt | grep "keyword" > filtered.txt
```
This combines piping and redirection. The cat command reads the content of file.txt, pipes it to grep to filter lines containing "keyword", and then redirects the filtered output to filtered.txt.
Example 5: Using /dev/null to Discard Output:
```bash
ls non_existent_folder 2> /dev/null
```
The 2> operator redirects the error output to /dev/null, effectively discarding the error message.
Example 6: Redirecting Input from Here Document:
```bash
grep -f - << EOF
```
pattern1
pattern2
EOF
This uses a here document to provide input to the grep command. The -f - flag tells grep to use patterns from standard input.
Outputs:
Let's see the outputs for some of the examples:
Example 1:
```bash
$ ls -l | grep ".txt"
```
-rw-r--r-- 1 user user 123 Aug 14 10:00 file1.txt
-rw-r--r-- 1 user user 456 Aug 14 11:00 file2.txt
Example 2:
```bash
$ cat file.txt | wc -l
```
10
Example 3:
```bash
$ sort < unsorted.txt > sorted.txt
```
Example 4:
```bash
$ cat file.txt | grep "keyword" > filtered.txt
```
Example 5:
```bash
$ ls non_existent_folder 2> /dev/null
```
Example 6:
```bash
$ grep -f - << EOF
```
> pattern1
> pattern2
> EOF
In these examples, you can see how piping and redirection are used to manipulate input and output streams, making your shell scripts more versatile and efficient.
