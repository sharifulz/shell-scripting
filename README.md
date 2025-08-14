# Shell Scripting Examples - Part 4

This document contains various shell scripting examples, each with copyable code blocks for GitHub README usage.

Interview Scripts
BACKUP DIRECTORY
Shell script that you can use to backup a directory using the tar command:
```bash
#!/bin/bash
# Source directory to backup
source_dir="/path/to/source/directory"
# Backup destination directory
backup_dir="/path/to/backup/directory"
# Backup filename with date
backup_filename="backup_$(date +%Y%m%d%H%M%S).tar.gz"
# Create the backup directory if it doesn't exist
mkdir -p "$backup_dir"
# Create the backup using tar
tar -czvf "$backup_dir/$backup_filename" "$source_dir"
# Check if the backup was successful
if [ $? -eq 0 ]; then
echo "Backup successful: $backup_filename created in $backup_dir"
else
echo "Backup failed"
fi
Make sure to replace /path/to/source/directory with the actual path of the directory you want to backup and /path/to/backup/directory with the desired backup destination. You can save this script to a file (e.g., backup_script.sh), give it execute permissions (chmod +x backup_script.sh), and then run it using ./backup_script.sh.
This script creates a compressed tar archive of the source directory and saves it in the backup directory with a filename that includes the current date and time. After the backup is created, it provides feedback on whether the backup was successful or not.
DEPLOYMENT-SCRIPT
Automating deployment using a shell script is a common practice in software development to streamline the deployment process and ensure consistency. You can use a shell script to automate tasks like pulling code from a repository, building the project, and deploying it to a server. Here's a general outline of how you could structure such a shell script:
#!/bin/bash
# Define variables
REPO_URL="https://github.com/yourusername/yourrepository.git"
TARGET_DIR="/path/to/deployment/directory"
BRANCH="main" # or the branch you want to deploy
BUILD_DIR="/path/to/build/directory"
# Update the code from the repository
echo "Updating code from the repository..."
cd "$TARGET_DIR" || exit
git pull origin "$BRANCH"
# Build the project (if needed)
echo "Building the project..."
cd "$BUILD_DIR" || exit
# Insert build commands here
# Deploy the project
echo "Deploying the project..."
# Insert deployment commands here
echo "Deployment complete!"
Here's a breakdown of the script:
1.
Shebang (#!/bin/bash): This line specifies the shell that will be used to interpret the script, in this case, Bash.
2.
Variable Definitions: Define variables for the repository URL, target deployment directory, branch to deploy, build directory, etc. Adjust these variables according to your project's specifics.
3.
Update Code: Change to the deployment directory, pull the latest code from the specified branch of the repository using git pull.
4.
Build Project: If your project requires building, change to the build directory and execute the necessary build commands. This could involve compiling code, installing dependencies, etc.
5.
Deploy Project: Execute commands to deploy the built project. This could involve copying files to the appropriate locations, restarting services, or any other deployment tasks.
6.
Completion Message: Output a message indicating that the deployment process is complete.
Remember to make the script executable using chmod +x scriptname.sh, where scriptname.sh is the name you give to your shell script.
Be cautious when automating deployment processes. Ensure that your script is well-tested in a non-production environment before deploying to production. Also, consider using version control and backup mechanisms to mitigate any potential risks.
Additionally, while shell scripts can be handy for simple automation, as your deployment process grows in complexity, you might want to explore more sophisticated automation tools such as Ansible, Jenkins, or container orchestration tools like Docker and Kubernetes.
FIND & REPLACE IN FILES
Shell script to perform a find and replace operation in multiple files using tools like sed (stream editor) or grep (with perl regex). Below is an example using sed to perform a find and replace operation:
#!/bin/bash
# Define variables
SEARCH_STRING="old_string"
REPLACE_STRING="new_string"
FILES_DIR="/path/to/files/directory"
# Perform find and replace using sed
find "$FILES_DIR" -type f -exec sed -i "s/$SEARCH_STRING/$REPLACE_STRING/g" {} +
echo "Find and replace complete!"
Here's how the script works:
1.
Shebang (#!/bin/bash): Specifies the shell to be used for interpreting the script.
2.
Variable Definitions: Define variables for the search string, replace string, and the directory where the files are located. Adjust these variables based on your needs.
3.
Perform Find and Replace: The find command searches for files in the specified directory ($FILES_DIR). For each file found, it runs sed -i to perform an in-place find and replace operation using the provided search and replace strings. The -i flag modifies the file in place.
The s/$SEARCH_STRING/$REPLACE_STRING/g argument to sed is the substitution pattern, where $SEARCH_STRING is replaced with $REPLACE_STRING. The g flag at the end ensures that all occurrences of the search string in each line are replaced.
4.
Completion Message: Outputs a message indicating that the find and replace operation is complete.
To use this script, replace the placeholders (old_string, new_string, /path/to/files/directory) with your actual values. Make the script executable using chmod +x scriptname.sh and then run it using ./scriptname.sh.
Keep in mind that this script performs find and replace operations across all files in the specified directory and its subdirectories. Make sure to test the script on a backup or in a controlled environment before using it on important files.
Monitoring System Resources with Shell
Shell script to monitor system resources such as CPU usage, memory usage, disk space, and more. The script can use built-in Unix commands like top, free, df, and others to gather information about system resources. Here's an example of a simple shell script to monitor system resources:
#!/bin/bash
while true; do
clear # Clear the terminal
echo "System Resource Monitoring"
echo "--------------------------"
# Display CPU usage
echo "CPU Usage:"
top -n 1 -b | grep "Cpu"
# Display memory usage
echo -e "\nMemory Usage:"
free -h
# Display disk space usage
echo -e "\nDisk Space Usage:"
df -h
sleep 5 # Wait for 5 seconds before the next update
done
Here's what this script does:
1.
Shebang (#!/bin/bash): Specifies the shell to be used for interpreting the script.
2.
while Loop: Creates an infinite loop that repeatedly gathers and displays system resource information.
3.
clear: Clears the terminal screen for a cleaner display.
4.
Display CPU Usage: Uses the top command with the -n 1 flag to display a single iteration of CPU usage information. The grep "Cpu" command filters out the relevant line.
5.
Display Memory Usage: Uses the free command with the -h flag to display memory usage in a human-readable format.
6.
Display Disk Space Usage: Uses the df command with the -h flag to display disk space usage in a human-readable format.
7.
sleep 5: Pauses the loop for 5 seconds before gathering and displaying resource information again.
To use the script, save it to a file (e.g., monitor_resources.sh), make it executable using chmod +x monitor_resources.sh, and then run it using ./monitor_resources.sh. The script will continually update and display system resource information in the terminal.
Keep in mind that this script is a basic example and may not provide real-time or highly detailed resource monitoring. For more comprehensive and advanced resource monitoring, you might consider using specialized tools like htop, nmon, sysstat, or other monitoring solutions.
Parsing & Text Processing
Let's say you have a text file named data.txt with the following content:
John Doe|25|Engineer
Jane Smith|30|Designer
Michael Johnson|28|Manager
And you want to parse and process this data using a shell script:
#!/bin/bash
# Read the text file line by line
while IFS='|' read -r name age profession; do
echo "Name: $name"
echo "Age: $age"
echo "Profession: $profession"
echo "---"
done < data.txt
```
Explanation:
1.
Shebang (#!/bin/bash): Specifies the shell to be used for interpreting the script.
2.
while Loop: Reads the text file line by line using the read command. The IFS='|' sets the input field separator to '|' so that the line is split into fields based on the '|' character.
3.
read -r name age profession: Reads the fields from each line and assigns them to the variables name, age, and profession.
4.
Display Information: Displays the extracted information using echo.
5.
< data.txt: Redirects the content of data.txt to the while loop's input.
When you run the script, it will output:
Name: John Doe
Age: 25
Profession: Engineer
---
Name: Jane Smith
Age: 30
Profession: Designer
---
Name: Michael Johnson
Age: 28
Profession: Manager
---
This is a simple example of parsing and processing a text file. Depending on your needs, you can include more advanced logic within the loop to perform actions like filtering data, performing calculations, or updating the file content.
Automation User Management with Shell Script
Automating user management tasks using a shell script can save time and ensure consistency when dealing with user accounts on a Unix-like system. Below is an example of a shell script that demonstrates how to automate user creation, modification, and deletion:
```bash
#!/bin/bash
# Define variables
ACTION="$1" # First argument: create, modify, or delete
USERNAME="$2" # Second argument: username
# Function to create a new user
create_user() {
if [ -z "$USERNAME" ]; then
echo "Usage: $0 create <username>"
exit 1
fi
useradd -m -s /bin/bash "$USERNAME"
echo "User $USERNAME created."
}
# Function to modify an existing user
modify_user() {
if [ -z "$USERNAME" ]; then
echo "Usage: $0 modify <username>"
exit 1
fi
usermod -s /bin/bash "$USERNAME"
echo "User $USERNAME modified."
}
# Function to delete an existing user
delete_user() {
if [ -z "$USERNAME" ]; then
echo "Usage: $0 delete <username>"
exit 1
fi
userdel -r "$USERNAME"
echo "User $USERNAME deleted."
}
# Main script
case "$ACTION" in
create)
create_user
;;
modify)
modify_user
;;
delete)
delete_user
;;
*)
echo "Usage: $0 {create|modify|delete} <username>"
exit 1
;;
esac
```
Explanation:
1.
Shebang (#!/bin/bash): Specifies the shell to be used for interpreting the script.
2.
Variables: The script takes two arguments: an action (create, modify, or delete) and a username.
3.
Functions: Separate functions are defined for each user management action (create, modify, delete). Each function includes relevant commands to perform the desired action using useradd, usermod, and userdel.
4.
Case Statement: The main part of the script uses a case statement to determine which user management action to perform based on the provided argument ($ACTION). It calls the corresponding function depending on the action.
To use the script, save it to a file (e.g., manage_users.sh), make it executable using chmod +x manage_users.sh, and then you can run it with the desired action and username as arguments. For example:
./manage_users.sh create johndoe
./manage_users.sh modify johndoe
./manage_users.sh delete johndoe
Be cautious when performing user management tasks, especially deletions, as they can have significant consequences. Always test your script in a controlled environment before using it in a production environment.
DATABASE-BAKUP
Automating database backups using a shell script is a common practice to ensure data integrity and disaster recovery. The example below demonstrates how to create a shell script to automate the backup of a MySQL database. This example assumes you have the mysqldump tool available, which is commonly used to create database backups.
```bash
#!/bin/bash
# Database credentials
DB_USER="your_username"
DB_PASS="your_password"
DB_NAME="your_database"
# Backup directory
BACKUP_DIR="/path/to/backup/directory"
# Date format for the backup file
DATE=$(date +"%Y-%m-%d_%H-%M-%S")
BACKUP_FILE="$BACKUP_DIR/$DB_NAME-backup-$DATE.sql"
# Create backup directory if it doesn't exist
mkdir -p "$BACKUP_DIR"
# Perform database backup using mysqldump
mysqldump -u "$DB_USER" -p"$DB_PASS" "$DB_NAME" > "$BACKUP_FILE"
# Check if the backup was successful
if [ $? -eq 0 ]; then
echo "Database backup successful: $BACKUP_FILE"
else
echo "Database backup failed"
fi
```
Explanation:
1.
Shebang (#!/bin/bash): Specifies the shell to be used for interpreting the script.
2.
Database Credentials: Replace your_username, your_password, and your_database with your actual database credentials and database name.
3.
Backup Directory: Set the BACKUP_DIR variable to the directory where you want to store your database backups.
4.
Date Format: Generates a timestamp in the format YYYY-MM-DD_HH-MM-SS to be used in the backup file name.
5.
Create Backup Directory: Creates the backup directory if it doesn't exist using mkdir -p.
6.
Database Backup: Uses the mysqldump command to create a backup of the specified database. The -u flag specifies the user, -p specifies the password (without a space), and the database name is provided. The output is redirected to the backup file.
7.
Check Backup Status: Checks the exit status of the mysqldump command. If the exit status is 0, the backup is considered successful. If it's not 0, the backup is considered failed.
Remember to secure your shell script by setting appropriate permissions (chmod +x scriptname.sh) and ensuring that the database credentials are kept secure. You can use additional options with mysqldump to specify more backup options such as excluding certain tables, using compression, and so on, based on your needs.
Test the script in a controlled environment before using it to automate database backups in a production environment.
File exists or Not
Shell script that checks if a specified file exists and prints a message if it does:
```bash
#!/bin/bash
# Specify the file path
FILE_PATH="/path/to/your/file.txt"
# Check if the file exists
if [ -f "$FILE_PATH" ]; then
echo "The file $FILE_PATH exists."
else
echo "The file $FILE_PATH does not exist."
fi
```
Explanation:
1.
Shebang (#!/bin/bash): Specifies the shell to be used for interpreting the script.
2.
FILE_PATH: Set the variable to the path of the file you want to check.
3.
if [ -f "$FILE_PATH" ]; then: This line checks if the file exists using the -f flag with the test command (also known as [).
4.
If the file exists, the script prints a message indicating that the file exists; otherwise, it prints a message indicating that the file does not exist.
To use the script:
1.
Save it to a file (e.g., check_file.sh).
2.
Make it executable using chmod +x check_file.sh.
3.
Update FILE_PATH with the actual path of the file you want to check.
4.
Run the script using ./check_file.sh.
The script will output the appropriate message based on whether the specified file exists or not.
