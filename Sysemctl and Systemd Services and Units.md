#LINUX/W9

# What is systemd?

- An init system and system manager that has widely become the new standard for Linux distros
- Not every distro uses systemd as its init system
	- if you see `bash: systemctl is not installed` then your machine doesn't use systemd
# What is systemctl?

- A command that is the central management tool for controlling the init system
- It can:
	- Manage services
	- Check statuses
	- Change system states
	- and work with configuration files
# Service Management

- Fundamental purpose of an init system is to initialize the components that must be started after the Linux kernel is booted (userland components)
- Init system also used to manager services and daemons for the server
- The target of most actions are called **units**
	- Units are categorized by the type of resource they represent and they are defined with files known as **unit files**
- For service management tasks, the target unit will be **service units** which have unit files with a suffix of `.service`
## Starting and stopping services

```
sudo systemctl start application.service
sudo systemctl start application # can do this too because systemctl knows to look for *.service
```
```
sudo systemctl stop application.service
```
## Restart or reload

Restart a running service
```
sudo systemctl restart application.service
```
Reload a service's config files without restarting
```
sudo systemctl reload application.service
```
Not all services can reload its config. Use this:
```
sudo systemctl reload-or-restart application.service
```
## Enabling and disabling
 
 To start a service at boot:
```
sudo systemctl enable application.service
```
- This will create a symbolic link from the system's copy of the service file (usually in `/lib/systemd/system` or `/etc/systemd/system`) into the location on disk where sytemd looks for autostart files
	- `/etc/systemd/system/some_target.target.wants`
	
To disable a service from starting automatically
```
sudo systemctl disable application.service
```
- This will remove the symbolic link that indicated that the service should be started automatically

- Keep in mind enabling a service does not start it in the current session
- Use `systemctl start` and `systemctl enable` if you want to start the service and have it automatically load on boot
## Checking status of services

To check the status of a service use the `status` command
```
systemctl status application.service
```
- This will provide you with service state, the cgroup hierarchy and the first few log lines

You can also check for specific states such as to see if a service is currently active
```
systemctl is-active application.service
```
- This will return the current unit state which is usually `active` or `inactive`
- Exit code will be 0 if active and 1 if inactive

To see if enabled
```
systemctl is-enabled application.service
```
- Output whether service is `enabled` or `disabled`
- Exit code 0 or 1 depending on answer

To see if in failed state
```
systemctl is-failed application.service
```
- This will return `active` or `failed` if an error occurred
- If unit was intentionally stopped it might return `unkown` or `inactive`
- Exit code 0 if failure occurred and 1 indicates any other status

# System State Overview

## Listing current units

To list all active units that systemd knows about
```
systemctl list-units
```
- Will output a list of all units that systemd currently has active on the system
![[Pasted image 20241107195617.png]]
- **UNIT**: The systemd unit name
- **LOAD**: Whether the unit's configuration file has been parsed by systemd.
	- The configuration of loaded units is kept in memory
- **ACTIVE**: Summary state about whether the unit is active
	- Usually a basic way to tell if unit started successfully or not
- **SUB**: This is a lower-level state that indicates more detailed information about the unit
	- Varies by unit type, state, and actual method in which unit runs
- **DESCRIPTION**: Short textual description of what unit is/does

```
systemctl
```
- Running this command alone will actually output the same thing as above `systemctl list-units`

```
systemctl list-units --all
```
- Will show any unit systemd loaded or attempted to load regardless of its current state on the system
- Some units become inactive after running, and some units that systemd attempted to load may not have been found on disk

```
systemctl list-units --all --state=inactive
```
- You can filter results by using the `--state` flag to indicate LOAD, ACTIVE, or SUB states that we wish to see
- Must keep `--all` flag so that systemctl allows non-active units to be displayed

## Listing all unit files

To see every available unit file within the systemd paths, including ones that systemd has not attempted to load
```
systemctl list-unit-files
```
![[Pasted image 20241107200903.png]]
- State will usually be enabled, disabled, static, or masked
- In this context, static means the unit file does not contain a install section, which is used to enable a unit


# Systemd timers

- Timers are systemd unit files whose name ends in .timer that control .service files or events
- Can be used as an alternative to cron
- Timer unit files include a \[Timer] section that define when and how the timer activates
- Two types of timers:
	1. Realtime timers - activates on calendar events
		- `OnCalendar=` is used to define them
	2. Monotonic timers - activate after a certain time span relative to a varying starting point
		-  These timers stop if the computer is suspended or shut down 
		- There are different types but `OnTypesec=` is used for all of them
		- `OnBootSec` and `OnUnitActiveSec` are common ones

## Service units

- For each .timer file, a matching .service file exists
- .timer file activates and controls the .service file
- .service does not require an \[Install] section as it is the timer units that are enabled

## Management

- To view all started timers run:
```
systemctl list-timers
```
- To use timers, enable and start them just like any other unit

## Example timers

A timer which will start 15 minutes after boot and again every week while the system is running
```
/etc/systemd/system/foo.timer

[Unit]
Description=Run foo weekly and on boot

[Timer]
OnBootSec=15min
OnUnitActiveSec=1w

[Install]
WantedBy=timers.target
```

A  timer which starts once a week (at 12:00am on Monday). When activated, it triggers the service immediately if it missed the last start time (option `Persistent=true`), for example due to the system being powered off
```
/etc/systemd/system/foo.timer

[Unit]
Description=Run foo weekly

[Timer]
OnCalendar=weekly
Persistent=true

[Install]
WantedBy=timers.target   
```
**OnCalendar** events use the following format:
```
DayOfWeek Year-Month-Day Hour:Minute:Second
```
- Example:
- Service run the first four days of each month at 12:00 PM, but **only** if that day is a Monday or a Tuesday
	- `OnCalendar=Mon,Tue *-*-01..04 12:00:00`

	