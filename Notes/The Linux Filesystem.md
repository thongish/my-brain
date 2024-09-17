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
	- Commonly used as the default filesytem for the majority of Linux distros
	- Supports significantly larger filesystems and individual file sizes compared to ext3
- **JSF**
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