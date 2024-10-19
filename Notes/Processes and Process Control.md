#LINUX/W3

# Executables versus processes

**Executable and Linkable Format** (ELF)
- The default executable file format on Linux and many other Unix-like systems
- ELF file stores executable code of programs (machine instructions loaded into memory)
- Can also store debug information
- ELF files can also be *linked* with other ELF files, known as **shared libraries**
	- Shared libraries are files that contain executable code but aren't meant to run as programs and only serve as collections of reusable functions
- You can see library linkage information with the `{bash}ldd` command
```
$ ldd /bin/bash
    linux-vdso.so.1 (0x00007ffc06ddb000)
    libtinfo.so.6 => /lib64/libtinfo.so.6 (0x00007f30b7293000)
    libc.so.6 => /lib64/libc.so.6 (0x00007f30b7000000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f30b743e000)
```
- ELF also stores metadata such as the target operating system and CPU architecture
```bash
echo '#!/bin/bash' >> hello.sh
echo 'echo "hello world"' >> hello.sh
chmod +x ./hello.sh
./hello.sh
hello world
```
- If a file has an executable bit (+x) on it and starts with a shebang line, the kernel will first load its interpreter (in this case, **/bin/bash**) and then give it the executable as an argument
- Once an executable file is loaded, directly by the kernel itself or with the help from an interpreter, it becomes a running **process**

# Process termination and exit codes

## Exit codes

- Every process terminates with an **exit code** - a numeric value that indicates whether it exited normally or terminated due to an error
	- By convention, a **zero** exit code means success, and any **non-zero** exit code means an error
	- There are no standard meanings for **non-zero** exits codes, their meanings vary between programs and operating systems
		- Many programs exit with **1** if they encounter an error, no matter the error
- In bash, you can find the exit code of the last command in a special variable named `{bash}$?`
```bash
true
echo $?
0
false
echo $?
1
```
- The simplest use case for exit codes is chaining commands with the **||** and **&&** operators
	- They can be called **on error** and **on success**
	- In **cmd1 || cmd2**, the shell will execute **cmd2** if **cmd1** fails (exits with a non-zero code)
	- In **cmd1 && cmd2**, the shell will execute **cmd2** only if **cmd1** succeeds (exits with a zero code)
```bash
touch /etc/my_file || echo "Fail!"
touch: cannot touch '/etc/my_file': Permission denied
Fail!
touch /tmp/my_file && echo "Success!"
Success!
```

## Signals

- A signal is a special condition that may occur during process execution
- There are many signals defined in the POSIX standard
	- Some are associated with specific program logic errors such as:
		- **SIGILL** - illegal instruction (ex. divide by zero)
		- **SIGSEV** - segmentation violation (trying to read or modify memory that wasn't allocated to the process)
	- Other signals are generated on external conditions to force a process to handle them, such as:
		- **SIGPIPE** - generated when a network socket or a local pipe is closed by the other end
	- These signals are only of interest to software devs, but some are designed as process control tools for administrators, such as:
		- **SIGINT** - interrupts a process
		- **SIGTERM** - asks the process to clean up its state and terminate
		- **SIGKILL** - tells the kernel to forcibly terminate a process
- The kernel has execution control when a signal is generated, not the process

# The kill command

-  The command for sending **signals** to processes is called **kill**
- You can send processes to the background by adding `&` to the end of a command
	- Using the `{bash}jobs` command you can see a list of background processes
		- This will return the job number and **process identifier** (PID)
	- Using `{bash}fg <job number>` you can bring a job with a certain number to the foreground
- When you press **Ctrl + C**, you are actually asking your shell to send it the running process a **SIGINT** signal - a signal to interrupt execution
	- If a process is in the background you can't use **Ctrl + C** to interrupt it, instead you use `{bash}kill <process id>` 
- By default, the `{bash}kill` command sends a **SIGTERM** signal
	- Both **SIGINT** and **SIGTERM** can be caught or ignored by a process
	- In order to force a process to quit, you should use `{bash}kill -SIGKILL <PID>`
		- or its numeric equivalent `{bash}kill -9 <PID>`
		- This should be a last resort
- If you run `{bash}kill -l` you will see a long list of available signals you can send

# The process tree

- Everything you launch from your shell becomes a **child process** of that shell process
- The shell itself is a child process 
	- either of the terminal emulator if you're on a Linux desktop
	- or of the OpenSSH daemon if you connected remotely over SSH
- There is a parent of all processes, and all running process relationships form a tree with a single root (PID = 1)
	- This is often called the **init process**
		- For a long time in general-purpose Linux distros, that process was **System V init**
- The PID=1 process can be anything
	- When you boot a Linux system, you can tell it which executable to load as PID=1
	- For example, you could append **init=/bin/bash** which would make your kernel drop into a single-user shell session instead of initiating its normal boot process
- Normally, the process with PID=1 serves as a service manager
- The **init** process is the only process that is launched directly by the kernel
	- Everything else is launched by the init process instead:
		- login managers,
		- SSH daemon,
		- web servers,
		- database systems
		- - everything you can think of
- You can view the full process tree with the `{bash}pstree` command
![[Pasted image 20240925220044.png]]

# Process search and monitoring

## The `{bash}ps` command

- **PS** is an abbreviation for **process selection** or **process snapshot**
	- It is a utility that allows you to retrieve and filter information about running processes
```
$ ps
    PID TTY          TIME CMD
 771681 pts/0    00:00:00 bash
 771705 pts/0    00:00:00 ps
```
- PID - process identifier - a unique number that the kernel assigns to each process when it's launched
- TTY - a terminal - can be:
	- a real serial console (**ttyS**\* or **ttyUSB**\*)
	- a virtual console on a physical display (**tty**\*)
	- or a purely virtual pseudo-terminal associated with an SSH connection or a terminal emulator (**pts/**\*)
- CMD - shows the command that was used to launch a process with its arguments, if any were used
- Two `{bash}ps` options you need to learn about right away are :
	- **a** - removes *owned by me*
	- **x** - removes *have a terminal*
	- A common command to view every process on the system is `{bash}ps ax`
```bash
ps ax
    PID TTY    STAT    TIME COMMAND
    1 ?        Ss    1:13 /usr/lib/systemd/systemd --switched-root --system --deserialize 30
    2 ?        S       0:01 [kthreadd]
    3 ?        I<      0:00 [rcu_gp]
    4 ?        I<      0:00 [rcu_par_gp]
               …
    509 ?      Ss      7:33 /usr/lib/systemd/systemd-journald
    529 ?      S       0:00 [jbd2/vda2-8]
    530 ?      I<      0:00 [ext4-rsv-conver]
    559 ?      Ss    226:16 /usr/lib/systemd/systemd-oomd
    561 ?      Ss      0:49 /usr/lib/systemd/systemd-userdbd
    562 ?      S<sl    1:17 /sbin/auditd
    589 ?      Ss      0:10 /usr/lib/systemd/systemd-homed
    590 ?      Ss      0:02 /usr/lib/systemd/systemd-logind
```
- STAT - the process state
	- **S** state means a process is in the interruptible sleep state - it waits for external events
	- **R** state means a process is currently doing something - running
	- **I** state is for idle kernel threads
	- **D** state is a process in uninterruptible sleep 
		- This state is concerning because uninterruptible sleep state processes are actively waiting for input/output operations to complete
		- If there are a large number of **D** state processes, it might mean the input/output systems are overloaded
- Processes with command names in square brackets are kernel services that are made to look like processes for ease of monitoring
- You can add **u** to your `{bash}ps` command if you want to see what users own each of the processes
	- `{bash}ps axu`

## Process monitoring tools

- `{bash}top` is a widely available tool in Linux distro repositories and is often installed by default in systems
	- It displays an interactive process list where the processes that consume the largest resources automatically floating to the top
- There are also other tools such as `{bash}htop` which offers different UI and additional functionality
- `{bash}top` and `{bash}htop` don't monitor resource usage types  
	- you can use `iotop` to monitor the input/output activity of processes

## The /proc filesystem

- Whenever a process is launched, the kernel adds a subdirectory named **/proc/PID/**
- It's good to know about the raw **/proc** interface, but it's impractical to use it as a source of process information
	- That's why we use `{bash}ps` and `{bash}pstree`


# Flash cards

What does ELF stand for?::**Executable and Linkable Format**
 

What are **shared libraries**?
?
Files that contain executable code but aren't meant to be run as programs
- Purpose is to serve as collections of reusable functions
 

What does `{bash}ldd` command do?
?
Prints shared library dependencies
```
$ ldd /bin/bash
    linux-vdso.so.1 (0x00007ffc06ddb000)
    libtinfo.so.6 => /lib64/libtinfo.so.6 (0x00007f30b7293000)
    libc.so.6 => /lib64/libc.so.6 (0x00007f30b7000000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f30b743e000)
```
 

What is an **exit code**?::A numeric value that indicates whether a process exited normally or terminated due to an error
 

What does a **zero** exit code usually mean?::The process successfully exited without any issues
 

What does a **non-zero** exit code usually mean?::The process exited with an error
 

How do you find the exit code of the last run command in bash?::`{bash}echo $?`
 

```bash
touch /etc/my_file || echo "Fail!"
touch /tmp/my_file && echo "Success!"
```
What is happening in each of these lines?
?
- The first line, the shell will only execute the second command if the first command exits with a **non-zero** exit code (a fail)
- The second line, the shell will only execute the second command if the first command exits with a **zero** exit code (a success)
 

What is a process **signal**?::A special condition that may occur during process execution
 

What is the **SIGILL** signal?::A signal sent to the process if there was an illegal instruction (i.e. divide by zero)
 

What is the **SIGSEV** signal?::Segmentation violation (trying to read or modify memory that wasn't allocated to the process)
 

What is the **SIGPIPE** signal?::A signal generated when a network socket or a local pipe is closed by the other end
 

What does the  **SIGINT** signal do?::Interrupts a process
 

What does the **SIGTERM** signal do?::Asks the process to clean up its state and terminate
 

What does the **SIGKILL** signal do?:: Tells the kernel to forcibly terminate a process
 

How do you send processes to the background?::Adding `{bash}&` to the end of a command
 

How do you see a list of background processes?::Using the `{bash}job` command
 

How do you bring a job (background process) into the foreground?::Using `fg <job number>`
 

What signal are you sending when you use **Ctrl + C**?
?
A **SIGINT** signal to interrupt the process
- You can't use **Ctrl + C** on background processes
	- You either have to bring them to the foreground or use `{bash}kill <process id>`
 

What signal does the `{bash}kill` command send to the process?::**SIGTERM**
 

What does the command, `{bash}kill -l` do?::Gives you a list of available signals you can send
 

What is PID=1?
?
The parent of all processes
- Often called the **init** process
 

What is the only process that is launched directly by the kernel?::The **init** process
 

What does the `pstree` command do?::Lets you view the full process tree
 

What is the `{bash}ps` command?
?
An abbreviation for **process snapshot** or **process selection**
- Retrieves a snapshot of running process information
 

The `{bash}ps` command outputs 3 columns:
- PID
- TTY
- STAT
- CMD
What does each of these mean?
?
- PID - Process identifier
- TTY - A terminal
- STAT - The process state
- CMD - The command that launched the process
 

What are the `a` and `x` in `{bash}ps ax`
?
- a - removes **owned by me**
- x - removes **has a terminal**
- `{bash}ps ax` is a common command to view every process on the system
 

What are the meanings of the STAT process states:
- **S**
- **R**
- **I** 
- **D**
?
- **S** - process is in an interruptible sleep state - waits for external events
- **R** - process is currently doing something - running
- **I** - for idle kernel threads
- **D** - process is in uninterruptible sleep
 

What does it mean when a process command name is in square brackets?::It's a kernel service that's made to look like a process for ease of monitoring
 

What does `{bash}ps -u` do?::Shows you what users own each process
 

What does the `{bash}top` command do?::Displays an interactive process list where the processes that consume most resources automatically float to the top
 

Whenever a process is launched, the kernel adds a sub-directory named...::**`/proc/<PID>/`**
 

