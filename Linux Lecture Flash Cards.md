
# Week-one flash cards
#LINUX/W1 


What is Linux?::A family of operating systems that use the Linux kernel

What is the Linux kernel?::The main component of a Linux OS and is the core interface that facilitates the communication between a computer's hardware and its processes

What does the Linux kernel do?
?
1. Memory management
	1. Keep track of how much memory is used to store what and where
2. Process management
	1. Determine which processes can use the CPU, when, and how long
3. Device drivers
	1. Act as mediator/interpreter between the hardware and processes
4. System calls and security
	1. Receive requests for service from the processes

What is the main difference between a server and desktop editions of Linux based OS?::Generally the only difference is the software installed on each of them

What is the distinction between a **terminal** and the **shell**?
?
- The terminal is an interface, the GUI that you interact with
- The shell is software that runs the commands you enter in the terminal

# Week-two flash cards
#LINUX/W2 

What is a **disk image**?
?
A file that contains an exact copy of the data and structure of a physical disk drive
- Like a snapshot of the disk, preserving everything from files and folders to the operating system and boot information

```bash
ssh -i -t -f -C
```
What do all these ssh command options do?
?
`-i` - identity_file: the path to the private key file associated with public key in the system you're SSHing into
`-t` - type: the type of encryption to use for the key
`-f` - filename: specify file name and location


# Week-three flash cards
#LINUX/W3 

What is a pseudo filesystem and an example of one?::A way to work with non-file data as though it were a file - /proc/ is an example of a pseudo filesystem

How do you create a new symbolic link?
?
Using the `ln` command with `-s`
```bash
ln -s <source_file> <symbolic_link>
```

# Week-four flash cards
#LINUX/W4 

What is the order that a Linux machine boots?
?
1. UEFI/BIOS
2. Boot Loader - GRUB, systemd-boot
3. Kernel
4. Init process - systemd, runit, r6, openRC

What does `{bash}ps -e` do?::Shows "every" process

What does `{bash}ps -o` do?
?
Let's you specify a format the command will output
```bash
ps -o pid, comm # ouputs PID and command only in the order specified
```

What does `{bash}ps -H` or `{bash}ps --forsest` do?::Prints out a hierarchy of the processes

What is the main difference between `{bash}find` and `{bash}grep`?
?
- `{bash}find` searches for files and directories based on file properties such as name, type, size, modification time, permissions, and more
- `{bash}grep` searches for patterns within the content of files or the standard output

What does the `{bash}-exec` option for `{bash}find` do?
?
Let's you perform commands on the files that `{bash}find` finds
```bash
find -type f -name "*.txt" -exec cat {} + # collect files, then run cmd
find -type f -name "*.txt" -exec cat {} \; # run cmd each file found
```
- These commands finds regular files in the current directory and cats them

# Week-five flash cards
#LINUX/W5 

How do you remove a user and their home directory?::`userdel -r <username>`

How can you kill all of a user's processes?::`pkill -u <username>`

# Week-six flash cards
#LINUX/W6

What is the difference between single and double quotes in bash scripts?
?
- Single quotes preserve the string literally; no expansion of variables or special characters happens
- Double quotes allow variable expansion, command substitution, and interpretation of escape characters
```bash
VAR="world"
echo 'Hello $VAR'   # Output: Hello $VAR (no expansion)
echo "Hello $VAR"   # Output: Hello world (variable expanded)
```

What do all of these positional parameters mean?
```bash
$0
$1, $2...
$$
$#
$@
$?
$!
$*
```
?
```bash
$0 - name of the bash script
$1, $2... - the bash script arguments
$$ - the process id of the current shell
$# - the total number of arguments passed to the script
$@ - the value of all the arguments passed to the script
$? - the exit status of the last executed command
$! - the process id of the last executed command
$* - all arguments treated as a single string
```

Can you nest an array inside of an array in bash?::No you can't

How do you create an indexed array?
?
```bash
declare -a arr=("1" "2" "3")
# or
arr=("1" "2" "3")
# Array items are separated by whitespace
```

How do you access values in an array?
?
```bash
#!/usr/bin/env bash
arr=("1" "two" "3")
# access by index
echo "${arr[0]}"
# print all of the array items
echo "${arr[@]}"
# print number of array items
echo "${#arr[@]}"
```

How do you create an associative array?
?
```bash
declare -A person
person["name"]="Jan"
person["age"]="31"
```

How do you access values and keys in an associative array?
?
```bash
# print all values
echo "${ex_arr[@]}"
# print all keys
echo "${!ex_arr[@]}"
# print value by key
echo "${ex_arr["key1"]}"
```



