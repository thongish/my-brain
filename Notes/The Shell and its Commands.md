#LINUX/W1
## Definitions

**Portable Operating System Interface** (POSIX)
- Defines standards for both the system and user-level application programming interfaces (APIs), along with command line shells and utility interfaces
## What is a shell?

- A shell is a program that receives commands and sends them to the operating system for processing
- Fundamental capability of shells is the ability to launch command line programs that are already installed on the system
	- Also offer built-ins and scripting control structures such as conditionals and loops

### Shells a Linux user can use

- **sh**: 
	- A POSIX-compatible Bourne shell
	- It is usually just bash running in compatibility mode
- **csh/tcsh**: 
	- Comes from the **Berkeley Software Distribution** (BSD) Unix system family 
	- Also available for Linux
	- Scripting syntax is similar to that of C and is incompatible with the Bourne shell
- **ksh**: 
	- A Bourne shell derivative
- **bash**: 
	- The most common Linux shell and was created for the GNU project
- **zsh** and **fish**: 
	- Highly customizable and feature-rich shells that are intentionally different from **sh** derivatives and require learning
	- Has large communities of enthusiasts

### Bash has the following features:

- Shell will check if a command is built-in before searching through a list of directories to locate the program
	- This set is known as the search path
	- You can view the search path by running `{bash}echo $PATH` command
	- You can create your own programs and call them by inputting their name
		- No matter what directory you are in, a program such as this will be found and launched if the program is in the **bin** directory
- To check the version of your shell, run the `{bash}echo $SHELL` command
- Majority of Linux commands are just programs that the shell runs
- Commands frequently have argument strings that could, for example, be filenames
	- ex. `{bash}cd ~/tmp`
		- This command switches to the **tmp** directory in your **home** directory
	- Multiple arguments are required for some commands
		- ex. `{bash}cp file1 file2` 
			- This command copies the first file to the second file
- The **flag** or option argument strings for some commands typically start with `{bash}-`
	- Flags change how the invoked program behaves
		- ex. `{bash}ls -lt`
			- The `{bash}-lt` here outputs a lengthy listing of files arranged by creation time
- **Wildcards** will be expanded by the shell to match file names in the current directory
	- ex. `{bash}ls -l *.sh`
		- Listing files named `anything.sh`
- **Standard input** (stdin) and **standard output** (stdout) are concepts that are followed by majority of Linux commands and programs
	- Programs receives a stream of data as **stdin** and produces a stream of output as **stdout**
	- Both connected to Terminal so that input is made via the keyboard and output is displayed on screen
	- Can reroute stdin and stdout using `{bash}cat` - an abbreviation for concatenate
		- ex. `{bash}cat /etc/passwd`
			- Shows content of one or more files without requiring you to open them for editing
- Ability to pipe data from one program's output to another's input using the `|` symbol
	- ex. `{bash}cat testfile.txt | wc -w`
		- Return content of the file and piping it to the `{bash}wc` command to count the number of words
	- ex. `{bash} cat testfile.txt | wc -l`
		- Counting the number of lines in the text file
- Create aliases for commands or groups of commands that are used frequently or difficult to type in
	- ex. `{bash}alias top10="du -hsx * | sort -rh | head -10"`
		- This sets an alias where you can just type `{bash}top10` in the terminal and it will run the commands in the quotation marks
- There are variables predefined in bash, such as `{bash}$HOME`
	- To see a list of assigned variables, use `{bash}set` command
- The **manual** (man) page is like a manual with instructions and descriptions about each command
	- ex. `{bash}bash-3.2$ man bash`
		- To view the man page for bash
- **Scripts** of shell commands can be written and called just like compiled programs 
	- ex.
```sh
#! /bin/bash

du -hsx * | sort -rh | head -10
```
Must run the chmod command to make the file executable
	- `{bash}chmod +x ~/bin/top10.sh`
	- To run it, `{bash}./top10.sh`
- Use `history` command to view history of executed commands
	- Run any command from the history by pressing `!` and the line number
		- ex. `{bash}!345`

# Basic shell commands

- `{bash}pwd` 
	- Used to determine which directory you are currently in
	- Abbreviation of **print working directory**
	- Prints the absolute path
- `{bash}mkdir <directory name>`
	- Make new directory
- `{bash}rmdir <directory name>`
	- Delete a directory
	- Can only be used to remove an empty directory
		- To remove both files and directories, use `{bash}rmdir -rf` (where `{bash}-rf`will recursively remove all the files and directories from inside the directory)
- `{bash}touch <file name>.txt`
	- Initial intent was to set the file modification date to the current time
	- Commonly used to make empty files 
- `{bash}ls`
	- See all files and directories inside current working directory
	- See hidden files `{bash}ls -a`
	- See all files and directories as a list `{bash}ls -la`
- `{bash}cp <file to be copied> <where to copy it>`
	- Copy files to a new file or directory
- `{bash}mv <file1> <file2>`
	- Can be used to move a file or directory from one location to another
	- Can also be used to rename a file
- `{bash}rm`
	- Used to remove files or directories 
	- `{bash}-r` or `{bash}-f` flags used to recursively remove a directory (`{bash}-r`) or force remove a  file or directory (`{bash}-f`)
- `{bash}locate`
	- Useful when you forget the location of a file
	- Using `{bash}-i` argument helps to ignore case sensitivity
	- `{bash}locate file1.txt` will find file path for file1.txt

# Intermediate shell commands

- `{bash}echo`
	- Display content that can be added to either a new or an existing file or to replace the content
	- `{bash}echo "content to be appended" >> file1.txt`
	- `{bash}echo "this content will replace" > file1.txt`
- `{bash}cat`
	- Used to read the content of a file
- `{bash}df`
	- Disk-free
	- Quickly view your filesystem and all mounted drives
	- Can see overall disk size, amount of space used, amount of space available, utilization percentage, and the partition that the disk is mounted on
	- Use with `{bash}-h` to make the data printed legible by humans
- `{bash}du`
	- Disk usage
	- Use to know the size of a specific directory or subdirectory
	- Use `{bash}sh` flag to provide a summary of a given item in human-readable form (the directory and all subdirectories)
- `{bash}uname`
	- Displays information regarding the operating system that your Linux distro is using
	- Majority of system information can be printed using `{bash}uname -a`
		- Displays kernel release date, version, processor type, and other related info
- `{bash}chmod`
	- Command used to modify special mode flags and access permissions of filesystem objects 
		- `{bash}chmod u-rwx, g=rx, o=r file1.txt`
			- u, g, o stands for user, group, owner
			- r, w, x stands for read, write, execute
			- = signifies *establish the permissions precisely like this*
		- `{bash}chmod 754 file1.txt`
			- Similar command using **octal permissions notation**
			- Each digit is the sum of the digits 4, 2, 1, and 0 
				- 4 = read
				- 2 = write
				- 1 = execute
				- 0 = no authorization
			- 7 = (4 + 2 + 1) give read, write, execute
			- 5 = (4 + 1) give read and execute
- `{bash}chown`
	- Change owner of system files and directories 
	- `{bash}chown thong:wheel <filename or directory name>`
		- Change ownership to the user `thong` and group `wheel`
- `{bash}chgrp`
	- Used if you're a non-privileged user and want to modify the group membership of your own file
- `{bash}man -k`
	- Searching man pages with keywords



# Flash cards

What is a shell?::A program that receives commands and sends them to the operating system for processing.
<!--SR:!2024-10-06,4,185-->

What is the fundamental capability of shells?
?
The ability to launch command-line programs already installed on the system.
- Also offers built-ins and scripting control structures such as conditional loops
<!--SR:!2024-10-05,1,145-->

What are some common Linux shells??
- sh, 
- csh/tcsh, 
- ksh, 
- bash, 
- zsh, 
- and fish

The "search path" in Linux refers to the list of directories that the system searches through to find executables. How can you view the search path in bash?
?
`{bash}echo $PATH`
<!--SR:!2024-10-16,13,225-->

How do you check your shell version?::`{bash}echo $SHELL`
<!--SR:!2024-10-08,6,225-->

What is the purpose of flags?
?
To change how the invoked program behaves.
- ex. `{bash}ls -lt`
	- The `{bash}-lt` here outputs a lengthy listing of files arranged by creation time
<!--SR:!2024-10-19,16,225-->

What are wildcards (`*`) used for?
?
To match file and directory name patterns
- ex. `{bash}ls -l *.sh`
	- Listing files named `anything.sh`
<!--SR:!2024-10-10,8,205-->

What is the cat command used for?::`{bash}cat /etc/passwd` (displays the contents of a file).
<!--SR:!2024-10-15,13,225-->

What is command piping?
?
Taking the output of one program and using it as an input for another program
-  ex. `{bash}cat testfile.txt | wc -w`
	- Return content of the file and piping it to the `{bash}wc` command to count the number of words
<!--SR:!2024-10-13,11,225-->

There are variables predefined in bash, such as `{bash}$HOME`, how do you see the list of all these variables?::Use the `{bash}set` command
<!--SR:!2024-10-24,20,250-->

What does `{bash}pwd` do?::Prints the absolute path of the current working directory.
<!--SR:!2024-10-20,17,245-->

How do you make a new directory?::`{bash}mkdir <directory name>`
<!--SR:!2024-10-24,20,250-->

How do you delete a directory?
?
`{bash}rmdir <directory name>` (can **only** remove an empty directory).
Using `{bash}rm <directory/file name>` is more practical
<!--SR:!2024-10-10,8,205-->

What command can be used to recursively remove directories and files?::`{bash}rm -rf <directory name>`
<!--SR:!2024-10-20,17,245-->

What is the purpose of `{bash}touch`?::To create an empty file or update the modification date of a file.
<!--SR:!2024-10-15,13,225-->

What does `ls` do?::Lists all files and directories in the current directory or specified directory
<!--SR:!2024-10-10,8,205-->

How can you see hidden files with `{bash}ls`?::`{bash}ls -a`
<!--SR:!2024-10-06,10,265-->

How do you list files with details using `{bash}ls`?::`{bash}ls -l`
<!--SR:!2024-10-16,13,225-->

How do you copy a file?::`{bash}cp <file to be copied> <where to copy it>`
<!--SR:!2024-10-20,17,245-->

How do you move or rename a file?::`{bash}mv <file1> <file2>` (can be used for both moving and renaming).
<!--SR:!2024-10-16,13,225-->

How do you remove a file?::`{bash}rm <file>`
<!--SR:!2024-10-20,17,245-->

What do the `{bash}-r` and `{bash}-f` flags in `{bash}rm` do?::`{bash}-r `removes directories recursively, and `{bash}-f` forces removal.
<!--SR:!2024-10-13,10,205-->

What is `{bash}locate` used for?::To find the path of a file on the system.
<!--SR:!2024-10-08,4,205-->

How can you make `{bash}locate` ignore case sensitivity?::`{bash}locate -i <file name>`
<!--SR:!2024-10-10,8,250-->

What is `{bash}echo` used for?::To print content to the terminal and write to a file.
<!--SR:!2024-10-24,20,250-->

How can you append content to a file with `{bash}echo`?::`{bash}echo "content to be appended" >> file1.txt`
<!--SR:!2024-10-20,17,245-->

How do you overwrite content in a file using `{bash}echo`?::`{bash}echo "this content will replace" > file1.txt`
<!--SR:!2024-10-07,4,225-->

What does `{bash}cat` do?::Reads and displays the content of a file to the terminal.
<!--SR:!2024-10-24,20,250-->

What does `{bash}df` do?
?
Disk-free
- Displays filesystem information like disk usage and available space.
<!--SR:!2024-10-07,4,190-->

How do you make `{bash}df` output human-readable?::`{bash}df -h`
<!--SR:!2024-10-07,4,225-->

What does `{bash}du` do?
?
Disk-usage
- Shows the size of a directory and its subdirectories.
<!--SR:!2024-10-08,4,205-->

How can you make `{bash}du` output human-readable?::`{bash}du -sh`
<!--SR:!2024-10-05,3,210-->

What does `{bash}uname` do?::Displays system information about the operating system.
<!--SR:!2024-10-16,13,225-->

How do you view detailed system information with `{bash}uname`?::`{bash}uname -a`
<!--SR:!2024-10-13,10,205-->

What does `{bash}chmod` do?::Changes file permissions for read, write, and execute.
<!--SR:!2024-10-24,20,250-->

What are the permission levels in `{bash}chmod`?
?
- 4 = read, 
- 2 = write, 
- 1 = execute, 
- 0 = no permission.
<!--SR:!2024-10-16,13,225-->

What is an example of a `{bash}chmod` command with octal notation?::`{bash}chmod 754 file1.txt`
<!--SR:!2024-10-20,17,245-->

How do you change a file's permissions to,
User = read/write
Group = read/write
Owner = read/write/execute
?
`{bash}chmod 667 file1.txt`
OR
`{bash}chmod u=rw,g=rw,o=rwx file1.txt`
<!--SR:!2024-10-15,13,225-->

What does `{bash}chown` do?::Changes the ownership of a file or directory.
<!--SR:!2024-10-20,17,245-->

How do you change the owner and group of a file?::`{bash}chown <user>:<group> <file or directory name>`
<!--SR:!2024-10-16,13,225-->

What does `{bash}chgrp` do?::Changes the group ownership of a file or directory.
<!--SR:!2024-10-13,10,210-->

How can you search man pages by keyword?::`{bash}man -k <keyword>`
<!--SR:!2024-10-08,12,245-->
