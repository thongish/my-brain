#LINUX/W2

# What is a filesystem?

- A filesystem is a name for the organizational framework and logical principles used to handle the names and groups of bits of data
- Filesystems govern the storage and retrieval of data in computers
- Without a filesystem, all the data saved on a computer's hard drive would be jumbled together
- With a filesystem, data is isolated and identified by breaking it up into pieces and giving each piece a name

## What types of Linux filesystems are there?

- **ext**
	- Extended filesystem
- **ext2**\
	- Second expanded system
- **ext3**
	- Upgraded version of **ext2**
	- Superior to ext2 because it is a **journaling** filesystem
		- Means if the computer/hard drive or both crash, the files can be repaired and restored upon reboot using a separate log that contains changes performed before the crash
	- 3 Levels of journaling
		- **Journal**
			- In the event of a power outage, the filesystem ensures effective filesystem recovery by writing both user data and meta data to the journal
			- The slowest ext3 journaling mode
			- Reduces the likelihood that any changes to any file in an ext3 filesystem will be lost
		- **Writeback**
			- Only metadata updates are logged in the journal
			- Data updates are written directly to their respective locations on the disk without being logged in the journal first
			- Provides better performance for write-intensive workloads because it reduces the overhead of journaling data
			- Not the best choice when data integrity is critical because it prioritizes performance over data consistency
		- **Ordered**
			- ext3's default journaling mode
			- Does not update related filesystem metadata
				- Instead, it flushes changes from file data to disk before updating the associated filesystem metadata
			- Only the files that were in the process of being written to the disk *disappear* in the event of a power outage
				- The architecture of the filesystem is undamaged
- **ext4**
	- Fourth extended system
	- Commonly used as the default filesystem for the majority of Linux distros
	- Supports significantly larger filesystems and individual file sizes compared to ext3
- **JFS**
	- Journaled File System
- **XFS**
	- Designed as a high-performance 64-bit journaling filesystem
	- Large file manipulation and high-end hardware performance are its strengths
- **Btrfs**
	- **copy-on-write** (COW) filesystem
	- Logging-style filesystem that links the change after writing the block modifications in a new area as opposed to journaling
	- New changes are not committed until the last write
- **Swap**
	- When memory is low, the system uses a swap file on the hard drive or SSD as temporary storage
	- Moves inactive program data from RAM tot he swap file, freeing up memory for other processes

- Linux is compatible with FAT and NTFS from other operating systems such as Windows

# The directory tree and standard directories

- To see the main structure of the root folder, use the command `{bash}tree -L 1`

- **/bin (Binaries)**:
    - Stores essential system binaries and commands.
    - Commonly used commands like `{bash}cd`, `{bash}mv`, and `{bash}pwd` are found here.

- **/boot**:
    - Contains bootloader files and boot configurations.
    - Often placed on a separate partition for dual-boot setups.

- **/dev (Devices)**:
    - Physical devices (hard drives, USBs, etc.) are represented here.
    - Partitions on devices may appear as `/dev/sda1`, `/dev/sda2`, etc.

- **/etc (Configuration)**:
    - System-wide configuration files are located here.
    - User-specific configs can be in `/home`, while global settings are in `/etc`.

- **/home (User Directories)**:
    - Contains personal user data and directories such as Desktop, Documents, etc.
    - Each user has their own folder, e.g., `/home/username`.

- **/lib (Libraries)**:
    - Stores essential system libraries required by programs and utilities.
    - Libraries often begin with `lib-`.

- **/media (External Media)**:
    - External devices like USB drives and CD-ROMs are mounted here.
    - Usage varies across different Linux distributions.

- **/mnt (Mount)**:
    - A generic mount point for drives or network locations.
    - Commonly used for temporary mounting of additional storage or network drives.

- **/opt (Optional Software)**:
    - Used for third-party software not managed by the system’s package manager.

- **/proc (Processes)**:
    - Contains system information and active process data.
    - Used for kernel-process communication.

- **/root (Root User Home)**:
    - Home directory for the root (superuser).
    - Special directory; avoid making changes unless necessary.

- **/sbin (System Binaries)**:
    - Stores binaries that are essential for system administration.
    - Commands here typically require superuser privileges.

- **/tmp (Temporary Files)**:
    - Temporary files are stored here and usually deleted on shutdown.

- **/usr (User Binaries and Utilities)**:
    - Contains user programs and utilities shared across users.

- **/var (Variable Data)**:
    - Stores files that dynamically change during system operations, such as logs and temporary data used by running processes.

![[Pasted image 20240916194448.png]]

# Links (hard and symbolic)

- Two alternative ways to refer to a file on the hard drive
	- **Hard links**
		- Refers to the inode of a file and is a synchronized carbon copy of that file
	- **Symbolic links**
		- Points directly to the file, which in turn points to the inode
			- A shortcut

## What is an inode?

- **Inodes** are data structures that Unix-style filesystems use to describe filesystem objects such as files and directories
- The properties and disk block locations of an objects data are stored in each inode
- Attributes of a filesystem object can include metadata, owner information, and permission information
- An operating system can obtain details about a file, including permission privileges and the precise location of the data on the hard drive using an inode

## What is a hard link?

- A special kind of link that points directly to a specific file by its name
- A hard link will continue to point to the original file even if the file's name is changed, unlike a soft link
- As opposed to symbolic links, hard links prevent files from being deleted or moved
- The **alias effect**, in which a file has numerous identifiers, can occur when multiple hard links point to the same file

## What are symbolic links?

- Are essentially shortcuts that refer to a file rather than the inode value of the file they point to
- This method can be applied to directories and can be used to make references to data that is located on a variety of hard discs and volumes
- A symbolic link will be broken or leave a dangling link if the original file is moved to a different folder
	- Due to the fact that symbolic links refer to the original file and not the inode value of the file
- Because symbolic links point to the original file, any changes you make to the symbolic link should result in corresponding changes being made to the actual file

# Mounting and unmounting filesystems

- For computers to access files, the filesystem must be mounted
- Use the `{bash}mount` command to show you what is mounted (usable) on your system at the moment
- To mount,
	- `{bash}mount <to be mounted> <mount directory>`
	- `{bash}mount /dev/sdb1 /mnt/mydrive`
- In order to have something mounted on reboot, you have to define the entry in `/etc/fstab`

## How to unmount the filesystem

- Using the `{bash}umount` command, you can detach the filesystem from your computer
	- `umount /dev/cdrom`

# Pseudo-filesystems

- A process information pseudo-filesystem is another name for the **proc** filesystem
- It contains runtime system information rather than *actual* files
	- System memory, devices mounted, hardware config, and so on
- Can be viewed as a kernel's command and information hub
- The **/proc** directory is accessed by many system utilities
	- The `{bash}lsmod` command lists the modules loaded by the kernel
	- the `{bash}lspci` command displays the devices attached to the PCI bus
	- Both of these commands are equivalent to 
		- `{bash}cat /proc/modules`
		- `{bash}cat /proc/pci` 
- Common examples of pseudo filesystems in Unix-like operating systems (Linux) include:
	- Processes, the most prominent use
	- Kernel information and parameters
	- System metrics, such as CPU usage

# Processes

- All the information about each running process can be found in the `/proc/pid` file

![[Pasted image 20240916202222.png]]

- A synthetic filesystem is a filesystem that provides a tree-like interface to non-file objects, making them look like regular files in a disk-based or long-term storage filesystem
	- This type of filesystem is known as a faux filesystem

# Kernel and system information

- Numerous folders under **/proc** contain a wealth of knowledge about the kernel and operating system

- - **/proc/cpuinfo**:
    - Contains detailed information about the CPU, including its specifications and capabilities.

- **/proc/meminfo**:
    - Displays information about the system's physical memory, including total memory, free memory, buffers, and caches.

- **/proc/vmstat**:
    - Provides statistics about the system's virtual memory, such as page faults, swap activity, and memory allocation.

- **/proc/mounts**:
    - Shows information about all currently mounted file systems, including device names, mount points, and file system types.

- **/proc/filesystems**:
    - Lists all file systems that are compiled into the kernel and kernel modules that are currently loaded.

- **/proc/uptime**:
    - Displays the system's uptime, i.e., how long the system has been running since the last boot.

- **/proc/cmdline**:
    - Contains the parameters passed to the kernel at boot time.

# CPU usage

- Use the command `{bash}top` to monitor CPU utilization

![[Pasted image 20240916202703.png]]




# Flash cards

What is a filesystem?
?
A framework used to organize and handle the storage and retrieval of data on computers.
- It identifies and isolates data by breaking it up into pieces and giving each piece a name
<!--SR:!2024-10-17,1,130-->

What is ext?::Extended filesystem.
<!--SR:!2024-10-23,14,230-->

What is ext2?::Second extended filesystem.
<!--SR:!2024-10-19,10,210-->

What is ext3?::An upgraded version of ext2 with journaling capabilities.
<!--SR:!2024-10-26,10,190-->

What is journaling in ext3?::A system that logs changes, allowing recovery and repair in case of crashes.
<!--SR:!2024-10-17,1,130-->

What are the three levels of journaling in ext3?::Journal, Writeback, and Ordered.
<!--SR:!2024-10-24,20,250-->

What is the Journal journaling mode?::Logs both user data and metadata for maximum recovery, but is the slowest.
<!--SR:!2024-10-19,10,210-->

What is the Writeback journaling mode?::Only logs metadata updates, prioritizing performance over data consistency.
<!--SR:!2024-10-18,2,150-->

What is the Ordered journaling mode?
?
ext3's default mode
- Ensures changes to file data are written to disk before updating metadata.
- Only files that were in the process of being written to the disk disappear in the event of a power outage
<!--SR:!2024-10-17,1,130-->

What is ext4?
?
Fourth extended filesystem, 
- used by most Linux distros
- supports larger files and filesystems compared to ext3.
<!--SR:!2024-11-15,30,230-->

What is JFS?
?
Journaled File System.
- 64-bit filesystem developed by IBM
<!--SR:!2024-10-19,10,210-->

What is XFS?
?
A high-performance 64-bit journaling filesystem.
- Its strengths are large file manipulation and high-end hardware performance
<!--SR:!2024-10-17,1,170-->

What is Btrfs?::A copy-on-write (COW) filesystem that logs changes after writing block modifications in new areas as opposed to journaling
<!--SR:!2024-10-18,2,150-->

What is Swap in Linux?::Temporary storage on the hard drive or SSD used when memory is low, moving inactive program data from RAM to disk.
<!--SR:!2024-10-26,10,190-->

Can Linux work with FAT and NTFS?::Yes, Linux is compatible with FAT and NTFS filesystems from Windows.
<!--SR:!2024-10-24,20,250-->

What is /bin?
?
Binaries 
- A directory storing essential system binaries and commands.
<!--SR:!2024-10-19,10,210-->

What is /boot?::A directory containing bootloader files and boot configurations.
<!--SR:!2024-11-15,30,230-->

What is /dev?
?
Devices 
- A directory representing physical devices like hard drives and USBs.
<!--SR:!2024-10-18,2,190-->

What is /etc?
?
Configuration 
- A directory containing system-wide configuration files.
<!--SR:!2024-11-15,30,230-->

What is /home?
?
User directories
- A directory storing personal user data and directories.
<!--SR:!2024-10-26,10,190-->

What is /lib?
?
Libraries
- A directory storing essential system libraries required by programs and utilities.
<!--SR:!2024-10-26,10,190-->

What is /media?
?
External media
- A directory where external devices like USB drives and CD-ROMs are mounted.
<!--SR:!2024-10-19,10,210-->

What is /mnt?
?
Mount
- A generic mount point for drives or network locations.
<!--SR:!2024-10-26,10,190-->

What is /opt?
?
Optional software
- A directory for third-party software not managed by the system’s package manager.
<!--SR:!2024-10-19,3,170-->

What is /proc?
?
Processes
- A directory containing system information and active process data.
<!--SR:!2024-10-20,4,190-->

What is /root?
?
Root user home
- The home directory for the root user (superuser).
<!--SR:!2024-10-29,20,250-->

What is /sbin?
?
System binaries
- A directory storing binaries essential for system administration.
<!--SR:!2024-10-18,2,170-->

What is /tmp?
?
Temporary files
- A directory for temporary files that are usually deleted on shutdown.
<!--SR:!2024-11-15,30,230-->

What is /usr?
?
User binaries and utilities
- A directory containing user programs and utilities shared across users.
<!--SR:!2024-10-19,10,210-->

What is /var?
?
Variable data
- A directory storing files that dynamically change during system operations.
<!--SR:!2024-10-17,1,130-->

What is a hard link?
?
A reference to the inode of a file, and is a synchronized carbon copy of that file.
- It points directly to a file and persists even if the file's name is changed
<!--SR:!2024-10-17,1,130-->

What is a symbolic link?::A shortcut pointing directly to a file, which in turn points to the inode.
<!--SR:!2024-10-18,2,150-->

What is an inode?
?
A data structure that Unix-style filesystems use to describe filesystem objects such as files and directories
- Properties and disk block locations of an object's data are stored in each inode
<!--SR:!2024-10-18,2,150-->

What happens to a symbolic link when the original file is moved?::The symbolic link breaks, resulting in a dangling link.
<!--SR:!2024-11-15,30,230-->

How do you mount a filesystem in Linux?::Use the `{bash}mount <to be mounted> <mount directory>` command.
<!--SR:!2024-11-15,30,230-->

How do you unmount a filesystem?::Use the `{bash}umount <mounted device>` command.
<!--SR:!2024-11-10,25,230-->

What is the /proc filesystem?::A pseudo-filesystem containing runtime system information.
<!--SR:!2024-10-19,10,210-->

What is a **synthetic filesystem**?
?
A filesystem that provides a tree-like interface to non-file objects, making them appear as regular files in a disk-based or long-term storage filesystem
- Also known as a **faux** filesytem
<!--SR:!2024-10-17,1,130-->

What does /proc/cpuinfo contain?::Detailed information about the CPU, including its specifications and capabilities.
<!--SR:!2024-10-26,10,190-->

What does /proc/meminfo contain?::Information about the system's physical memory, including total and free memory.
<!--SR:!2024-10-26,10,210-->

What does /proc/vmstat contain?::Statistics about the system's virtual memory, such as page faults and swap activity.
<!--SR:!2024-10-26,10,190-->

What does /proc/mounts contain?::Information about all currently mounted file systems.
<!--SR:!2024-10-26,10,210-->

What does /proc/filesystems contain?:: Information about all file systems compiled into the kernel, and currently loaded kernel modules.
<!--SR:!2024-10-18,2,150-->

What does /proc/uptime contain?::The system’s uptime since the last boot.
<!--SR:!2024-10-19,10,210-->

What command shows CPU utilization?::`{bash}top`
<!--SR:!2024-10-29,20,250-->
