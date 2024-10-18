#LINUX/W4 

# Some commands for managing users and groups

- `{bash}adduser` - Adds a user to the system
- `{bash}userdel` - Delete a user account and related files
- `{bash}addgroup` - Add a group to the system
- `{bash}delgroup` - Remove a group from the system
- `{bash}usermod` - Modify a user account
- `{bash}chage` - Change password expiration time and see user password expiry information
- `{bash}passwd` - Create or change a user account's password
- `{bash}sudo` - Run one or more commands as another user (get root privileges)
	- Typically with superuser permissions by running `{bash}sudo su <username>`
- `{bash}su` - Become the root user

## Files relevant to these operations

- `/etc/passwd` - User information / account properties
- `/etc/shadow` - Encrypted passwords / password properties
- `/etc/group` - Group information
- `/etc/sudoers` - Configuration for `{bash}sudo`

## /etc/passwd structure

```
<username>:<x>:<UID>:<GID>:<Comment>:<Home directory>:<Default shell>
```
- `<username>` and `<Comment>` are self-explanatory
- `<x>` is the "shadowed" password for the user
- `<uid>` and `<GID>` include integers that respectively, reflect the `<usernameprimary>` group IP and user ID
- `<Home directory>` displays absolute path to the home directory of the user
- `<Default shell>` is the shell that is made available to the user when they log in

# How to add a new user account

- Two commands that do essentially the same thing but in different ways
	- `{bash}adduser`
	- `{bash}useradd`
## useradd

```bash
sudo  useradd -d /home/packt -m packt
```
- Set up user with the name **packt**
- `{bash}-d` option confirms we want the user to have a home directory
	- /home/packt is the argument given to `{bash}-d` to specify the home directory path
- `{bash}-m` option is used to tells the system to create the user's home directory otherwise none will be created even when using `{bash}-d`
```bash
sudo passwd packt
Changing password for user packt.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```
- `{bash}sudo passwd packt` command can be used to set a password for the newly created account **packt**

## adduser

- `{bash}adduser` will create everything for you, including the home directory, group, and password
```bash
sudo adduser packt2
Adding user `packt2' ...
Adding new group `packt2' (1004) ...
Adding new user `packt2' (1003) with group `packt2' ...
The home directory `/home/packt2' already exists.  Not copying from `/etc/skel'.
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for packt2
Enter the new value, or press ENTER for the default
        Full Name []:
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n]
```
- Command copies files from `/etc/skel`
	- `/etc/skel` - provides the backbone or skeleton of what any new account `/home/<username>` would look like
- Sets the user's home directory to `/home/packt2` by default
- User account is also assigned the next available **User ID** (UID) and **Group ID** (GUID) of 1004

- Both `adduser` and `useradd` copies files from the `/etc/skel` directory but `adduser` is somewhat more detailed in the tasks that it executes

# How to delete an account

- Deleting accounts when a user no longer needs access to the system is highly necessary because unmanaged accounts frequently become a security concern
- Before deleting the account, need to ask yourself whether you might need that user's files some time in the future
	- User files are often duplicated and archived for long-term preservation
- Most businesses have a policy set in place for the retention of user's data in the event they depart the organization
```bash
sudo userdel packt2
```
- `{bash}userdel` does not delete the user's home directory
- If you want to delete the user along with its home directory you user the `{bash}-r` option
```bash
sudo userdel -r packt2
```
- Once directory is deleted, the files cannot be recovered if there is no backup

- Deleting a user account in Linux involves:
	- Backing up data,
	- Terminating processes, 
	- Removing the user from groups,
	- Deleting the home directory,
	- Updating system files,
	- and performing a final cleanup

# Understanding the /etc/sudoers file

- To let an ordinary user account carry out user administration operations we need to make a special permissions entry for the user, **packt**, in the `/etc/sudoers` to allow it special access:
```
packt ALL=(ALL) ALL
```
- First, state the user which the rule will apply to (packt)
- All hosts that use the same `/etc/sudoers` file are covered by the rule if the first **ALL** is present
	- Since the same file is no longer shared among different machines, this term now refers to the current host
- **(ALL) ALL** informs us that any user may execute any command as the **packt** user
	- In terms of functionality, this is similar to **(root) ALL**

- Important to manage permissions using groups because it makes life easier
	- Simpler to remove a user from the **sudo** group rather than removing the user from 100 different places

# Switching users

- Using the `{bash}su` command to switch to an account with superuser privileges
- You can make changes to the user's home folder, default shell, and the ability to add a description to the user account can be made with the `usermod` command

- Initially, the `/etc/passwd`file looks like this:
```bash
grep packtdemo /etc/passwd
packtdemo:x:1004:1005:,,,:/home/packtdemo:/bin/bash
```
- To add a description and change the default shell:
```bash
sudo usermod --comment "Demo account for packt" --shell /bin/sh packtdemo
grep packtdemo /etc/passwd
packtdemo:x:1004:1005:Demo account for packt:/home/packtdemo:/bin/sh
```

- Often useful to be able to switch to the user account of a person having issues with accessing certain files or directories and being able to view the issue yourself and test whether your solution resolves their problem

- `{bash}su` alone switches to another user while maintaining the current environment
- `{bash}su -` simulates a complete login environment for the target user
	- Including setting up their home directory and environment variables and starting a new login shell

# Managing account passwords

## Locking/unlocking user accounts

- You can lock and unlock accounts using the `{bash}passwd` command
	- For example, if a person is going to be gone for awhile, you can lock their account so it's inaccessible to other users while they're gone
```bash
sudo passwd -l packt # locks the user packt

sudo passwd -u packt # unlocks the user packt
```

## Setting password expiration

- The `chage` command lets us change the length of time a user's password is valid
	- Also provides a more user-friendly way to read the `/etc/shadow` file to view current password expiration information
```bash
sudo chage -l packt
```
- It's not necessary to use `chage` with `{bash}sudo` command if you're viewing expiration information of your own login
	- You do need to use `{bash}sudo` if you want to view information of any other user account though
![[Pasted image 20241003191627.png]]
- You can force users to change their password upon first successful login by setting their total number of days before password expiration to 0 using:
```bash
sudo chage -d 0 packt
```
- The following command allows you to configure a user account so that it will demand a new password after a particular number of days have passed:
```bash
sudo chage -M 90 <username>
```
- This command configures the user account to become invalid after 90 days and to demand a new password at that time

# Group management

- Group management is very useful on Linux because you can grant or deny access to files or directories by adding/removing them from a group the file/directory belongs to\
- Every file/directory on Linux has both a user and a group that claims ownership of it
	- Just one user and one group associated with every file/directory
```bash
cat /etc/group
```
- Useful command to see what groups are currently active on the system
	- The structure  of each line is as follows
	- `<Group name>:<Group password>:<GID>:<Group members>`
		- Group passwords are not used if there is an **x** next to `<Group password>`
- To create a group, use:
```bash
sudo addgroup <groupname>
```
- To delete a group, use 
```bash
sudo delgroup <groupname>
```


- You can use the `usermod` command to associate users with groups
```bash
sudo usermod -aG packtgroup packt
```
- This command adds the user **packt** to the **packtgroup** group
- `{bash}-aG`
	- The `{bash}-a` means **append** the user to the group without removing them from any other group
	- the `{bash}G` flag specifies the group name
- If you want to modify the primary group that a user belongs to,
```bash
sudo usermod -g <groupname> <username>
```
- Groups are the easiest way to manage security permissions
	- Imagine removing one user from a group assigned to 100 resources rather than removing the user 100 times

# Permissions

- File permissions give owners, group members, and everyone else access to read from, write to, or execute files
- Following commands are used to manage ownership and set permissions:
```bash
chmod - change file permissions
chown - change the file owner
chgrp - change group ownership
id - print the user and group IDs
```

```bash
echo "This is a test file" >  testfile
ls -l testfile
-rw-rw-r-- 1 packt packt 20 Feb  6 16:37 testfile
```
- First character denotes that it is a normal file (not a directory or type of system object)
- Next nine characters show the read (r), write (w), and execute (x) permissions for the owner, group owner, and other users

## Changing groups

```bash
sudo chgrp <group name> <file to change ownership>
```

```bash
sudo usermod -aG <group name> <user>
```

```bash
sudo chown <user> <file to change ownership>
```

- Three additional permissions:
	- setuid - Set user ID
		- Allows users to execute a file using the file owner's permissions, rather than their own
		- Ex. `passwd` command lets users change their passwords but this file is owned by root (the superuser)
			- With the **setuid** bit, any user can run `passwd` and change only their own password
		- `{bash}sudo chmod u+s <filename>`
	- setgid - Set group ID
		- Allows users to run a file using the group's permissions, instead of their own
		- When **setgid** is set on a directory, any file created inside it inherits the directory's group ownership
			- Helpful for shared group projects
		- `{bash}sudo chmod g+s <filename>`
	- Sticky bit
		- Most useful on directories in shared environments
		- Ensures that only the file's owner , the directory's owner, or the root user can delete or modify the files in that directory
			- This way, users can't delete or alter each other's files in a common directory
```bash
# for sticky bit
sudo mkdir packtdir
sudo chmod +t packtdir
```

## More /etc/sudoers

- Back to `/etc/sudoers`, we can grant superuser access to every user in a group
- `/usr/bin/updatedb %packtgroup ALL=(ALL)`
	- This command specifies that users who belong to **packtgroup** are permitted to run **updatedb** (/usr/bin/updateb)
	- Group must be preceded with a % sign, which is the only distinction between group members and individual users
- `{bash}sudo -l` - display the calling user's permitted commands in `/etc/sudoers`


# Flash cards

How do you add or delete a user to the system?
?
- `{bash}adduser`
- `userdel`

How do you add/remove a group to the system?
?
- `addgroup`
- `delgroup`

Where can you find user account information or properties?::/etc/passwd

What is the /etc/shadow file?::Encrypted passwords / password properties

What is the /etc/group file?::Group information

What is the /etc/sudoers file?::Configuration for `{bash}sudo`

What is the difference between `useradd` and `adduser`?
?
- `useradd` requires manual configuration of things like password, home directory, etc
- `adduser` is a more user-friendly command that does all those things for you

What is /etc/skel?::A directory that provides the folder scheme for new accounts

What can you do with the `usermod` command?::Modify user account things such as home folder, default shell, add description to user, associate with group, etc

How do you add a user to a group?
?
```bash
sudo usermod -aG group thong
# -a means append to group without removing them from other groups
# -G specifies the group name
```

What does the `{bash}su`  command do?
?
- Switch to an account with superuser privileges
- `{bash}su -` does the same thing but simulates a complete login environment for the target user

How do you lock or unlock user accounts?
?
- `{bash}sudo passwd -l <user>` - locks account
- `{bash}sudo passwd -u <user>` - unlocks account

What does the `chage` command do?::Change the length of time a user's password is valid

How many users and groups can a file belong to?::One user and one group per file

What are the three additional permissions besides read, write, execute?
?
- setuid - allows users to execute a file using the file owner's permissions, rather than their own
- setgid - allows users to run a file using the group's permissions, instead of their own
	- When set on a directory, any file created inside it inherits the directory's group ownership
	- This is helpful for shared group projects
- sticky bit - ensures that only the file/directory's owner can delete or modify the file or directory
