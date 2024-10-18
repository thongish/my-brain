#LINUX/W6 

# Shift

- **Shift** is used to shift positional parameters to the left
- It can take a number (n) argument to shift the positional parameters **n** times

```bash
#!/bin/bash
echo the script has $# arguments. # $# is a variable that returns number of arguments passed into script

echo print $1
shift # moves positional parameters once to left
echo print $1
shift 3 # moves positional paramaters 3 times to left
echo print $1
```
- If we run this script with arguments # 1-5 like `script 1 2 3 4 5`, the output would be:
```
the script has 5 arguments.
print 1
print 2
print 5
```

# Here documents

I dont understand this shit

# Using functions

- Two ways to define functions in bash:
```bash
function_name () {
	# commands here
}

function function_name {
	# commands here
}
```
- Functions are local to the script where they are executed
- Bash-wide functions exist and are initialized from the Bash startup scripts
	- Use `set` to show a list of all functions available
	- Use `unset` to remove a function

## Function arguments

- Bash functions can work with arguments, which have a local scope within the function
```bash
#!/bin/bash
hello () {
	echo hello $1 # $1 is a placeholder in this function
}
hello bob # this command provides bob as an argument
```
- Function arguments are not affected by passing positional parameters to a script while executing it

# Using case

- **case** used to check a specific number of cases, similar to Python's `match`
- Useful to provide scripts that work with certain specific arguments
- case is case sensitive
```bash
#!/bin/bash

echo are you good?

read GOOD # read will take an input from the user and assign it to variable GOOD

GOOD=$(echo $GOOD | tr [:upper:] [:lower:]) # this line reassigns GOOD using command substitution to chance case of the string

case $GOOD in 
yes|oiu) # using just the closing parenthesis, you can define multiple different cases in one line or just one case. Pipe | to separate cases
	echo "that's nice"
	;; # indicates the end of the condition
no)
	echo "that's not nice"
	;;
*) # if $GOOD doesn't fit any of those cases, run this. Similar to else in python
	echo okay
	;;
esac # case inversed to end the case

```

# Working with options

- An **option** is an argument that changes script behaviour
	- Think of `ls -l` changing the output of ls to include more details
- You can write your script to take options and arguments using `getopts` and `case`:

```bash
#!/bin/bash
while getopts "ab:" opts; do # the : after b tells the script that option -b can take an argument
# evaluate options a and b, and while evaluating them, put them in a temporary variable opts
	case $opts in # define what should happen if a specific option is encountered
	a)
		# do something
		;;
	b)
		# do something
		;;
	esac
done
```

# Using variables in functions

- No matter where variables are defined, they always have a global scope, even if defined in a function
- Use `local` keyword to define variables with a local scope inside of a function
```bash
my_function () {
	local var2=B # scope is within function
	var1=A # global scope
}
```