### 5.2 Shell Scripts and IDE

**Core Bash Script Components:**
- **Shebang**: Indicates the shell to execute the script. Options:
    - `#!/bin/bash` (traditional, but `/bin` is not standard anymore)
    - `#!/usr/bin/env bash` (preferred, ensures bash from the environment)
- Shebang tells the system what program or shell should be used to interpret the script

**Commenting**:
- Comments explain the script’s functionality.
- Essential for maintainability and readability, even for your future self.

**Whitespace**:
- Use white lines to increase readability.

**Script Structure**:
- **Simple scripts**: A list of commands.
- **Complex scripts**: Separate code into blocks for different phases of execution.

**Script Naming**:
- No required extensions, but `.sh` is often used for convenience, especially for non-Linux users.
- Examples: `.sh` for bash, `.csh` for c-shell.

**Script Location**:
- By default, scripts can’t be executed from the current directory (security feature).
- Store personal scripts in `~/bin` and modify the `PATH` accordingly. For global scripts, use `/usr/local/bin` (requires `sudo` privileges).

---

#### Working with Git & First Script Example
1. **Git Installation**:
    - Ubuntu: `sudo apt install git`
    - Red Hat: `sudo yum install git`
    - Arch: `sudo pacman -S git -y`
2. **Cloning a Repository**:
    - Example: `git clone https://github.com/sandervanvugt/bash-scripting`
    - Repository content may evolve; current examples are not meant to be perfect but teach through analysis.

`

---

#### Running a Simple Script (Hello World)
1. **Script Basics**:
    - Starts with shebang (`#!/usr/bin/env bash`)
    - Comments at the top.
    - White lines for readability.
    - End with `exit 0` (exit status of 0 means success, though often not necessary).
2. **Running the Script**:
    - By default, scripts can't run from the current directory (`./` needed).
    - Fix permissions with `chmod +x` to make the script executable.
3. **Exit Codes**:
    - The last command sets the exit code, viewable with `echo $?`.
    - Example: Using `exit 5` to return a custom exit code.


### 5.4 Running the Scripts
 **Setting Execute Permission**:
- To run a script as a separate program, set execute permission
```bash
chmod +x myscript
```
- Replace `myscript` with your script's name.

**Ownership**:
- You must be the owner of the file to change its permission.
- If you create a script, you are usually the owner.
- You cannot change permissions for files you do not own due to security reasons.

 **Running Scripts**:
- If the script's directory is **not** in the `$PATH` variable, run it using:
```bash
./myscript
```

- Scripts can also be run as an argument to the shell, e.g.:
```bash
bash myscript
```
- This way, execute permissions are not required, and the `$PATH` variable is not needed since Bash is the executable.
-  Editing a script: `nvim file-name.ext`
- Changing permissions to run script: `chmod +x file-name.ext`
- Checking permissions: `ls -l myscript.sh
- Can also use for temporary: `bash ./file-name.ext`

**Shebang Consideration**:
- The **shebang** (`#!`) at the beginning of the script specifies which interpreter to use.
- If you use `bash` to run a script that is intended for another shell, the shebang is ignored.
- **Best Practice**: Always include a shebang in the first line of your script and place it in a directory included in the `$PATH`. Avoid running it as an argument to the Bash shell.

Here are concise notes summarizing the key points from the video about using variables and the `read` command in shell scripts:

---
### 6.3 Defining and Using Variables

**Local vs. Environment Variables**:
- **Local variables**: Work only within the current shell.
- **Environment variables**: Part of the operating system, set during boot.

**Arrays**:
- Arrays are special multi-valued variables, which will be covered in detail later.

**Data Types in Bash**:
- Bash does not use specific data types (numbers, strings, characters).
- Variable behavior remains consistent regardless of data type.

**Declare Command**:
- `declare` sets variable attributes, not data types.
- Example: `declare -r ANSWER="yes"` creates a read-only variable.
- `declare -a MYARRAY` defines an indexed array.
- Use `declare -p` to display the type and attributes of variables (e.g., `declare -p GROUPS` vs. `declare -p PATH`).

**Variable Scope**:
- Variables are local to the current shell.
- Use `export key=value` to make variables available to subshells.
- Clear variable contents with `key=`.
- Remove a variable entirely using `unset`.

**Examples of Declaring Variables**:
- **Defining**: `key=value` (e.g., `color=red`).
- **Exporting**: `export key=value` for subshells (e.g., `export color=blue`).
- **Listing variables**: Use `env` for environment variables.

**Variable Usage**:
- Use `$` before a variable name to access its value.
- Best practice: Enclose variable names in curly braces (e.g., `${color}`) to avoid ambiguity.
- Mandatory curly braces when appending values or performing operations on variables.

 **Special Variables in Bash**:
- `$RANDOM`: Generates a random number.
- `$SECONDS`: Displays the number of seconds the shell has been running.
- `$LINENO`: The current line in a script.
- `$GROUPS`: Lists the groups the current user belongs to.
- `$DIRSTACK`: Shows the stack of visited directories.
- Standard variables like `$BASH_ENV`, `$BASHOPT` contain environment-related information.

**Creating a Simple Script with Variables**:
- Always begin a script with `#!/bin/bash`.
- Define variables at the top for clarity (e.g., `COLOR="red"`).
- Example:

```bash
COLOR="red" 
TREE="oak" 
echo "The $TREE is $COLOR"
```


### 6.4 Defining Variables with `read`

**Defining Variables**:
- Variables can be defined directly in scripts or by using the `read` command.

 **Using `read`**:
- The `read` command makes a shell script interactive, pausing execution to take user input.
- User input is stored in a variable provided as an argument to `read`.
- Example:
```bash
echo "Enter a value:" 
read value
echo you have entered $value
```

**Automatic Variable**:
- If no variable name is specified, input is stored in the automatically assigned variable `REPLY`.

 **Press Enter to Continue**:
- `read` can be used without arguments for prompts like "Press enter to continue":
```bash
echo "Press enter to continue" 
read
```

**Reading Multiple Variables**:
- You can read multiple values simultaneously:
```bash
echo "Enter first name, last name, and city:" 
read first_name last_name city
echo nice to meet you $firstname $lastname from $city
```
- The variables can then be used in the script.

**Example Script**:
- **Script 2**: An example of using `read` to change directories:
```bash
echo "Which directory do you want to go to?" 
read dir 
cd "$dir"  # Navigate to the specified directory 
pwd        # Show the current directory 
ls         # List contents of the directory
```

**Permissions**:
- Ensure scripts have execute permission using:
```bash
chmod +x script_name
```

 **Subshell Behavior**:
- Running a script starts a subshell, and changes made (like `cd`) only affect that subshell.
- When the script ends, you return to the original shell.

**Example with User Input**:
- Example script prompting for a first name, last name, and city:
```bash
echo "Enter first name, last name, and city:" 
read first_name last_name city 
echo "Nice to meet you, $first_name $last_name from $city."
```

**Handling Input Issues**:
- When reading multiple variables, if more input is provided than variables, the extra input goes into the last variable.
- Quotes do not effectively solve this problem for `read`.

**Best Practices**:
- Include a shebang (`#!`) at the start of your script for proper syntax highlighting and to specify the interpreter.

### 8.2 Using `if` Statements 

**Purpose of `if`**:
- The `if` statement checks whether a condition is true.
- A condition is a command that returns an exit status:
- **Exit Status 0**: Condition is true.
- **Exit Status 1**: Condition is false.

**Basic Structure**:
- Syntax:
```bash
if [ condition ]; then
# commands 
fi
```

- Example:
```bash
if true; then     
	echo "Command executed successfully" 
fi
```
- The `then` keyword introduces the commands to be executed if the condition is true.

**One-liners**:
- You can use a one-liner format for simple commands:

```bash
if test -f /etc/hosts; then echo "File exists"; fi
```
- Use semicolons to separate commands in one-liners.

**Nesting and Multiple Commands**:
- `if` statements can contain multiple commands and can be nested:
```bash
if [ condition ]; then     
	if [ another_condition ]; then
		# nested commands     
	fi 
fi
```

**Example Command Line Script**:
- Create a simple script:
```bash
if false; then     
	echo "Command executed successfully" 
fi
```
- Use `chmod +x simple-if` to make the script executable.

**Using Commands in Conditions**:
- Example using a command that generates an exit status:
```bash
if grep student /etc/passwd; then
	echo "Command executed successfully" 
fi
```

**Redirecting Output**:
- To suppress command output, redirect it to `/dev/null`:
```bash
if grep student /etc/passwd > /dev/null; then
	echo "Command executed successfully" 
fi
```
- The `-s` option for `grep` can also be used for silent operation.
 
 **Checking File Existence**:
- Check if a file exists:
```bash
if [ -f /etc/hosts ]; then
	echo "File exists" 
fi
```

**Else Statement**:
- The `else` statement can be added to handle cases where the condition is false.

### 8.4 Testing with `[[]]` #watch
**Introduction to Double Square Brackets**:
- Double square brackets (`[[ ]]`) are used for conditional testing in Bash.
- They offer enhanced functionality compared to single square brackets (`[ ]`), which were originally external commands.

**Compatibility**:
- Single square brackets (`[ ]`) are compatible across all shells, making them a preferred choice for portability in scripts.
- Double square brackets are Bash-specific and may not work in other shell environments.

**Enhanced Features**:
- Double square brackets allow for more complex tests that are not possible with single brackets.

Examples include:
- String comparisons without the need for quotes:
```bash
if [[ $var1 == "yes" && $var2 == "red" ]]; then     
	echo "Condition met" 
fi
```

- Integer comparisons:
```bash 
if [[ 1 -lt 2 ]]; then     
	echo "1 is smaller than 2" 
fi
```

**Checking File Existence**:
- Double brackets simplify checks for file existence, even if file names contain spaces:
```bash
if [[ -e $B ]]; then
	echo "$B exists" 
fi
```

**Logical Tests**:
- You can perform complex logical tests with double square brackets:
```bash
if [[ $var == IMG* && ($var == *.png || $var == *.jpg) ]]; then
	echo "$var starts with IMG and ends with PNG or JPG" 
fi
```
- This example checks if a variable starts with `IMG` and ends with either `.png` or `.jpg`.

**Preference for Simplicity**:
- Despite their capabilities, many scripters prefer to use single brackets for simplicity and compatibility reasons.

### 8.6 Using `if`...`then`...`else`... with `elif`

**Introduction to `elif`**:
- `elif` (else if) allows you to add additional conditions to an `if` statement.
- It provides a way to check multiple conditions sequentially.
2. **Syntax Structure**:

- The basic structure includes an `if` statement, followed by one or more `elif` statements and an optional `else`:
```bash
if [ condition1 ]; then     
	# Commands if condition1 is true 
elif [ condition2 ]; then     
	# Commands if condition2 is true 
else     
	# Commands if neither condition is true 
fi
```

**Example of Usage**:
- An example script, **numcheck**, prompts the user to input three numbers and checks which number is the largest:
```bash
if [ $num1 -ge $num2 ] && [ $num1 -ge $num3 ]; then     
	echo "$num1 is the largest number." 
elif [ $num2 -ge $num1 ] && [ $num2 -ge $num3 ]; then     
	echo "$num2 is the largest number." 
else     
	echo "$num3 is the largest number." 
fi
```
- This structure allows for clear comparisons between the numbers.

 **Running the Example**:
- For inputs like `5`, `3`, and `1`, the output is "5 is the largest number."
- For inputs like `1`, `2`, and `3`, the output is "3 is the largest number."

 **Cautions with `elif`**:
- While `elif` is powerful, excessive nesting of `if` statements can lead to complex and unreadable scripts.
- Confusing scripts are harder to troubleshoot, so it’s best to keep logic straightforward.

### 9.2 Using `for`

**Introduction to `for` Loops**:

- The `for` loop is used to iterate over a range of items, making it useful for handling sequences of numbers or files.

**Basic Syntax**:
- A simple example demonstrates iterating through a range:
```bash
for i in {115..127}; do     
	echo $i 
done
```

- This prints numbers from 115 to 127.

**Practical Application**:
- Instead of just echoing, commands can be used, such as pinging a series of IP addresses:
```bash
for i in {115..127}; do     
	ping -c 1 192.168.29.$i 
done
```
- This performs a ping sweep, checking the availability of devices in that range.

**Example of Grading Script**:
- The video discusses a grading script used in RHCSA classes that checks user configurations:
- It uses `grep` to check for user existence in `/etc/passwd`:
```bash
for i in user1 user2 user3; do     
	grep $i /etc/passwd > /dev/null 
done
```
- If a user does not exist, the script outputs an error message.
- The script also checks for file existence in user home directories.

**Additional Features**:
- The script uses `passwd -s` to display password settings, checking if passwords are locked.
- It mentions using `sshpass`, which allows SSH connections from the command line without password prompts, although it's not directly related to the `for` loop.

**Encouragement to Explore**:
- The presenter encourages viewers to learn from the script, experiment with creating users, and understand the script's functionality.