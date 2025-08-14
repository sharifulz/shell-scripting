# SHELL SCRIPTING
In Linux, a shell is a command-line interface that allows users to interact with the operating system and execute various commands. It's both a user interface and a scripting language that provides a way to communicate with the computer system through textual commands. The shell is a type of program called an interpreter.
SHELL
- BASH
- PYTHON
- SH
- ZSH
## Shebang
The shebang (#!) is a special sequence of characters at the beginning of a script file that tells the operating system which interpreter should be used to execute the script. It's followed by the path to the interpreter binary. This is particularly useful for shell scripts to ensure they're executed by the correct shell, even if the user's default shell is different.
For example, in a Bash shell script, the shebang line would be:
```bash
#!/bin/bash
```
Let's break down this example:
- #!: This is the shebang sequence that indicates the start of the shebang line.
- /bin/bash: This is the path to the Bash interpreter binary. It tells the system to use the Bash interpreter to execute the script.
Here are a few points to note about the shebang:
1. The shebang line is not required for all scripts, but it's a good practice to include it, especially for shell scripts.
2. The shebang line must be the very first line of the script file.
3. The path after the shebang (/bin/bash in the example) points to the interpreter that should be used. It should be the absolute path to the interpreter.
4. The shebang line doesn't introduce a comment. It's a directive for the system to determine how to execute the script.
5. Different shells or interpreters may have their own paths in the shebang line, such as /usr/bin/python for Python scripts or /usr/bin/env node for Node.js scripts.
Including the appropriate shebang line ensures that your script is executed by the correct interpreter, regardless of the default shell of the user running the script.
## Basic Example of Shell Script
```bash
#!/bin/bash
```
# Prompt the user for their name
```bash
echo "Hello! What's your name?"
```
read name
# Greet the user
```bash
echo "Nice to meet you, $name!"
```
To use this script:
1. Save it to a file (e.g., greeting_script.sh).
2. Make it executable using chmod +x greeting_script.sh.
3. Run the script using ./greeting_script.sh.
To install Docker using a shell script, you can use the following script for a Linux system. This example is based on installing Docker on Ubuntu using the official Docker repository:
```bash
#!/bin/bash
```
# Update package index and install required dependencies
```bash
sudo apt update
```
```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```
# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
# Add Docker repository
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
# Install Docker
```bash
sudo apt update
```
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io
```
# Add the current user to the 'docker' group to run Docker commands without 'sudo'
```bash
sudo usermod -aG docker $USER
```
# Start and enable Docker service
```bash
sudo systemctl start docker
```
```bash
sudo systemctl enable docker
```
# Print Docker version
docker --version
Explanation:
1. Shebang (#!/bin/bash): Specifies the shell to be used for interpreting the script.
2. Update Package Index: Updates the package index and installs necessary dependencies.
3. Add Docker's GPG Key: Adds Docker's official GPG key for secure package installation.
4. Add Docker Repository: Adds Docker's official repository to the system's sources list.
5. Install Docker: Installs Docker Community Edition (CE) packages.
6. Add User to Docker Group: Adds the current user to the 'docker' group to run Docker commands without needing 'sudo'.
7. Start and Enable Docker: Starts the Docker service and enables it to start on system boot.
8. Print Docker Version: Prints the installed Docker version.
To use the script:
1. Save it to a file (e.g., install_docker.sh).
2. Make it executable using chmod +x install_docker.sh.
3. Run the script with superuser privileges using sudo ./install_docker.sh.
Please note that this script is tailored for Ubuntu. If you're using a different Linux distribution, you might need to adjust the package management commands and repository configuration accordingly. Always verify scripts from reliable sources and review them before execution, especially when dealing with system-level changes.
# Shell Scripting Hands-On
Variables and data types in shell scripting, along with examples:
1. Declaring Variables: In shell scripting, you can declare variables without specifying their data types. Variables are case-sensitive and can consist of letters, numbers, and underscores, but they must start with a letter or underscore. Here's how you declare a variable:
variable_name=value
2. Variable Types: Shell scripting doesn't have strict data types like other programming languages. Variables are treated as strings by default, but you can manipulate them to behave as different types.
3. Variable Assignment and Manipulation: You can assign values to variables using the assignment operator =. Here are examples of various types of variable assignments and manipulations:
# String Variable
name="John"
```bash
echo "Hello, $name!" # Output: Hello, John!
```
# Integer Variable
age=25
```bash
echo "Age: $age years" # Output: Age: 25 years
```
# Arithmetic Operations
x=10
y=5
sum=$((x + y))
```bash
echo "Sum: $sum" # Output: Sum: 15
```
# Concatenation
greeting="Hello"
subject="World"
message="$greeting, $subject!"
```bash
echo $message # Output: Hello, World!
```
# String Length
string="Shell Scripting"
length=${#string}
```bash
echo "Length: $length" # Output: Length: 15
```
# Substring Extraction
substring=${string:0:4} # Extracts first 4 characters
```bash
echo "Substring: $substring" # Output: Substring: Shell
```
4. Command Substitution: You can capture the output of a command and assign it to a variable using command substitution. There are two ways to do this:
# Using Backticks
current_date=`date`
```bash
echo "Current date: $current_date"
```
# Using $(...)
current_time=$(date +%H:%M:%S)
```bash
echo "Current time: $current_time"
```
5. Readonly Variables: You can declare variables as readonly to prevent their values from being changed after initial assignment:
readonly pi=3.14159
pi=3.14 # This will result in an error
6. Unsetting Variables: You can unset (delete) a variable using the unset command:
unset variable_name
7. Quoting Variables: Quoting variables properly is essential to preserve spaces and special characters:
variable="Hello World"
```bash
echo "Using double quotes: $variable"
```
```bash
echo 'Using single quotes: $variable'
```
```bash
echo Using no quotes: $variable
```
```bash
echo "Using double quotes: '$variable'"
```
8. Escaping Characters: If you need to include special characters within a variable, you can escape them using backslashes:
special_char="\$"
```bash
echo "Variable: $special_char" # Output: Variable: $
```
Sure, let's delve into shell scripting with a focus on reading user input and input validation. Shell scripts are a series of commands that are executed in a sequence. User input allows scripts to interact with users and make decisions based on that input. Input validation ensures that the provided input meets certain criteria.
Reading User Input: To read user input in a shell script, you can use the read command. It reads input from the user until the Enter key is pressed and assigns the input to a variable. Here's an example:
```bash
#!/bin/bash
```
# Prompt the user for their name
```bash
echo "Please enter your name:"
```
read name
# Display a greeting using the user's input
```bash
echo "Hello, $name! Nice to meet you."
```
In this example, the user's input is stored in the name variable, and the script uses that input to display a greeting.
Input with Prompting: You can also use the read command with a prompt message directly, eliminating the need for separate echo commands:
```bash
#!/bin/bash
```
# Read input with a prompt message
read -p "Enter your favorite color: " color
```bash
echo "Your favorite color is $color."
```
Using read Options: The read command has various options to customize its behavior. For example:
- -p specifies a prompt message.
- -r disables interpreting backslashes, useful for reading file paths.
- -t sets a timeout for input.
- -s hides input (useful for passwords).
```bash
#!/bin/bash
```
# Read password without echoing characters
read -s -p "Enter your password: " password
```bash
echo "Password entered."
```
# Read input with timeout
read -t 5 -p "Enter something in 5 seconds: " timed_input
```bash
echo "You entered: $timed_input"
```
## Conditional Statements
Conditional statements allow your script to make decisions and execute different code paths based on certain conditions.
1. if, else, elif:
The if statement is used to execute code block(s) conditionally. You can use else to define what should be done if the condition is not met, and elif to add more conditions.
```bash
#!/bin/bash
```
num=10
if [ $num -gt 10 ]; then
```bash
echo "Number is greater than 10"
```
elif [ $num -eq 10 ]; then
```bash
echo "Number is equal to 10"
```
else
```bash
echo "Number is less than 10"
```
fi
Case Statements (Switch):
The case statement allows you to compare a variable against multiple values and execute code based on the match.
```bash
#!/bin/bash
```
fruit="apple"
case $fruit in
"apple")
```bash
echo "It's an apple"
```
;;
"banana")
```bash
echo "It's a banana"
```
;;
"orange")
```bash
echo "It's an orange"
```
;;
*)
```bash
echo "Unknown fruit"
```
;;
esac
## Looping
Looping structures help you repeat a set of commands multiple times.
1. for Loop:
The for loop iterates over a list of items and performs the specified commands for each item.
```bash
#!/bin/bash
```
for color in red green blue; do
```bash
echo "Color: $color"
```
done
2. while Loop:
The while loop repeatedly executes a block of code as long as a condition is true.
```bash
#!/bin/bash
```
count=1
while [ $count -le 5 ]; do
```bash
echo "Count: $count"
```
((count++))
done
3. until Loop:
The until loop is similar to the while loop but continues executing until a condition becomes true.
```bash
#!/bin/bash
```
num=0
until [ $num -ge 5 ]; do
```bash
echo "Number: $num"
```
((num++))
done
Sure, I'd be happy to explain shell script functions in detail, along with examples for each of the topics you mentioned.
