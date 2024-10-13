#LINUX/W5 
# Core bash script ingredients

- Best practice - make sure your script always include the following:
	- `#!/bin/bash` or `#!/usr/bin/env bash` to identify Bash as the script interpreter
		- This is called a shebang
		- `#!/usr/bin/env bash` is the better way to identify Bash because it takes Bash from your environment and it'll find the variable that points you to the correct Bash shell
			- No matter where your Bash shell is installed, it will always work
	- Comment to explain what the script is doing
		- Explains for other users and yourself what the script is doing
	- White lines increase readability
	- Different blocks of code to easily distinguish between parts of the script
## Script names

- Script names are arbitrary
-  Extensions are not required but may be convenient for scripts users from non-Linux operating systems
## Script location

- Because of Linux **$PATH** restrictions, scripts cannot be executed from the current directory
- Consider using **~/bin** to store scripts for personal use
	- If doing this, modify **$PATH** as it's not in the path for every distribution
- Consider using **/usr/local/bin** for scripts that should be available for all users
	- This requires sudo privileges

## Other stuff

- Run `./<script name>` to execute the script in the current directory
	- You need to first give the script execute permission to do this, 
		- `chmod +x <script name>`
		- You need to be owner of the script to use this method unless you use sudo privileges
- If the script is in your **$PATH**, you can run the script by just calling the script file name,
	- `<script name>`
- You can also start the script as an argument to the shell (Bash) `bash <script name>`
	- You don't need execute permissions for this method and $PATH is not needed
	- This is not best practice because if you run the script as an argument to the shell, the shell ignores the shebang
# Defining and using variables

- Local variables work in the current shell only
- The environment variable is an operating system setting that is set while booting
- Arrays - special multi-valued variables

## Bash variable data types

- Bash variables don't use data types
- Variables can contain a:
	- number,
	- character, 
	- string of characters
- Bash does not change behaviour according tot he type of data in a variable
- `declare` can be used to set specific variable attributes
	- `declare -r ANSWER=yes` sets $ANSWER as a read-only variable
	- `declare [-a|-A] MYARRAY` is used to define an indexed or associative array
	- `declare -p` to find out which type of variable something is
- Using `declare` is NOT required to set a variable, but may be required to set an array

## Defining variables

- Defining a variable can be easy: `key=value`
- Variables are not case sensitive
	- Environment variables are written in uppercase by default
	- Local variables can be written in any case
- After defining, a variable is available in the current shell only
- To make variables available in subshell also, use `export key=value`
- To clear variable contents, use `key=`
	- Wipes value of the variable without deleting the variable itself
- You can delete the variable completely by using `unset key`
- Use `env` to get access to environment variables
- You can set variables to be available to all shells by adding it to **.bashrc** directory

## Using variables

- To use the current value assigned to a variable, put a `$` in front of the variable name
- Recommended, but not mandatory, to put the variable name between { }
```
color=red
echo $color
echo ${color}
```
- Why use { }?
	- You can do pattern matching operators on the variable to change the value of the variable if using { } 
	- Or, perform an operation on the value of the variable while working with it, the { } are mandatory
	- Also, append anything directly after the name of the variable, you need to use curly braces 
		- `echo ${color}1` will output `red1`
- To avoid confusion on specific types of variables, it is recommended (not mandatory) to put the variable name between double quotes
```
echo "${color}"
```
- Assign the variables at the top of the script
## Special variables

- Bash works with some special variables, that have an automatically assigned value
```
$RANDOM - prints a random number
$SECONDS - number of seconds the shell has been running
$LINENO - the line in the current script
$HISTCMD - the number of this command in history
$GROUPS - an array that holds the names of groups that the current user is a member of
$DIRSTACK - list of recently visted directories, also use dirs to display
```

# Using simple **if** statements

- `if` is used to verify that a condition is true
```
if true
then
	echo command executed successfully
fi
```
- `true` is also a command that happens to generate exit code 0 by default
	- It's a simple test which will always evaluate to exit status 0
- `then` introduces the commands you are going to run if the condition is true
- `fi` ends the if statement
- The condition is a command that return an exit code 0, or a test that completed successfully
	- `if [ -f /etc/hosts ]; then echo file exists; fi`
- You can redirect the output of a command you are testing by appending `>/dev/null` to the if statement
	- This will avoid side effects like printing to the terminal
```
if grep thong /etc/passwd >/dev/null
then
	echo command executed successfully
fi
```

# Testing with `[[ ]]`

- A regular test is written as `[ condition ]`
- Enhanced version is written as `[[ condition ]]`
	- This is a Bash internal, and offers features not offered by **test**
	- Because it is a Bash internal, you may not find it in other shells

## Examples

- `[[ $VAR1 = yes && $VAR2 = red]]` is using a conditional statement within the test
- `[[ 1 < 2]]` tests if 1 is smaller than 2
- `[[ -e $b ]]` will test if $b exists. If $b is a file that contains spaces, using `[[ ]]` won't require you to use quotes
- `[[ $var = img* && ($var = *.png) || $var = *.jpg) ]] && echo $var starts with img and ends iwth .jpg or .png`

# Using if then else with `elif`

- `elif` can be added to the if/then/else statement to add a second condition
```
if [ -d $1 ]; then
	echo $1 is a directory
elif [ -f $1 ]; then
	echo $1 is a file
else
	echo $1 is an unknown entity
fi
```

# Using `for`

- `for` is used to iterate over a range of items
- This is useful for handling a range of arguments, or a series of files
```bash
for i in {115..127}; do echo $i; done
# prints numbers 115 to 127 line by line
for i in {115..127}; do ping -c 192.168.29.$i; done
# pings every ip address ending in 115 to 127 to check if an IP address exists

for value in values
do
	# do something
done
```
