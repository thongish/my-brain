Kevin Pham A01026954
Godriele Dela CruzA01341131

## Q1:

Our answer
```
#!/bin/bash

# We think this line intitializes x as an integer
((x=5)) # Initialize x

# Loop runs 3 times
for ((i=0; i<3; i++)); do

	# multiplies x by 2 each loop
	((x *= 2)) # Double x in each iteration
	
	# prints the value of X after multiplication minus 1
	echo $((x - 1)) # Output x - 1

	# this line takes the output of each loop and adds to the variable sum and prints the sum when the loop ends. 
	
	# We think sed checks the last digit of the sum to see if it's an even number and will replace it with the word "odd"
	
	# rev will reverse the order of the output from sed and then cut will cut from index 1-3 from the output with index starting at 1
	
done | awk '{sum+=$1} END {print sum}' | sed 's/[02468]$/odd/' | rev | cut -
c 1-3
```

Chatgpt answer
```
#!/bin/bash

# Initialize x with the integer value 5
((x=5))

# Loop runs 3 times
for ((i=0; i<3; i++)); do

	# Double x in each iteration
	((x *= 2))
	
	# Output the value of x minus 1
	echo $((x - 1))

# Take the output of each loop, add it to a variable called sum, and print sum when the loop ends.
# sed replaces the last even digit of the sum with "odd" if it is even.
# rev reverses the string, and cut captures the first three characters of the reversed output.

done | awk '{sum+=$1} END {print sum}' | sed 's/[02468]$/odd/' | rev | cut -c 1-3
```


## Q2:

Our answer
```
#!/bin/bash

# This line initializes an associative array
declare -A arr=( [0]=1 [1]=1 [2]=2 )

# Loops 3 times
for ((i=0; i<3; i++)); do

	# Reassinging the value of the key at i= iteration loop number to itself added to itself multiplied by 2
	arr[$i]=$((arr[$i] + i * 2))
done

# prints the values of each value in the associative array
# transforms spaces into a new line
# sort -n is sorting the number values 
# uniq -c is going to count repeating numbers and then awk is going to multiply those counts together and then head will only display the first 2 lines, tail will only take the last line
# xargs is similar to -exec for the find command, it'll echo the string 
echo "${arr[@]}" | tr ' ' '\n' | sort -n | uniq -c | awk '{print $2 * $1}' |
head -n 2 | tail -n 1 | xargs -I{} echo "{} squared is {}"
```

Chatgpt's answer
```
#!/bin/bash

# Initializes an indexed array with values at indices 0, 1, and 2
declare -A arr=( [0]=1 [1]=1 [2]=2 )

# Loop runs 3 times
for ((i=0; i<3; i++)); do

	# Update arr[i] by adding i * 2 to the current value of arr[i]
	arr[$i]=$((arr[$i] + i * 2))
done

# Outputs each array value on a new line, sorts them numerically, counts occurrences of each unique number, 
# multiplies each unique number by its count, and extracts the second result. Then formats the final output.
echo "${arr[@]}" | tr ' ' '\n' | sort -n | uniq -c | awk '{print $2 * $1}' |
head -n 2 | tail -n 1 | xargs -I{} echo "{} squared is {}"

```

## Q3:

Our answer
```
# there's a semi colon somewhere it doesn't belong
bash: syntax error near unexpected token `;'
```

Chatgpt answer
In terms of `awk` specifically, common causes for this error are:

- A misplaced or extra semicolon within the `awk` command.
- Incorrect syntax when passing `awk` commands in a `bash` script (e.g., missing quotes around the `awk` command or forgetting to escape special characters).

## Q4:

Our answer
```
# We think the order of the command and its options might be wrong
bash: /usr/bin/somecommand: cannot execute binary file: Exec format error
```

Chatgpt answer

**Possible causes include:**

- The binary is for a different architecture than the current system.
- The file is not a valid executable file format for the current system.
- The command path or file permissions are incorrect, though this is less common for this specific error.