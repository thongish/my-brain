# cloud-init

- cloud-init is an open source initialization tool designed to make getting pre-configured systems up and running easier and with minimum effort
- Most commonly used by developers, system administrators and other IT professionals to automate configuration of:
	- VMs
	- cloud instances
	- or machines on a network

# What is the benefit of cloud-init?

- Whenever you deploy a new cloud instance, cloud-init takes an initial configuration that you supply, and automatically applies those settings when the instance is created
	- The real power of cloud-init comes from the fact that you can re-use these configurations as often as you want, and always get consistent, reliable results

# What does cloud-init do?

- Handles a range of tasks that normally happen when a new instance is created
- Responsible for activities like,
	- setting the hostname, 
	- configuring network interfaces,
	- creating user accounts, 
	- and ever running scrips

# How does cloud-init work?

- The operation of cloud-init broadly takes place in two separate phases during the boot process
	- The first phase is during the early (local) boot stage, before networking has been enabled
	- The second phase is during the late boot stages, after cloud-init has applied the networking configuration
## During early boot

- In this pre-networking stage, cloud-init discovers the data sources, obtains all the configuration data from it, and configures networking
	- **Identify the data source**
		- Hardware is checked for built-in values that will identify the data source your instance is running on 
		- The data source is the source of all configuration data
	- **Fetch the configuration data**
		- This configuration data tells cloud-init what actions to take
		- This data can take the form of:
			- **Metadata** about the instance, such as machine ID, hostname and network config
				OR
			- **Vendor data** and/or **user data**
				- Both of these take the same form, but **vendor data** is provided by the cloud vendor, and **user data** is provided by the user
				- These data are usually applied in the post-networking phase, and might include:
					- Hardware optimizations
					- Integration with the specific cloud platform
					- SSH keys
					- Custom scripts
	- **Write network configuration**
		- cloud-init writes the network configuration and configures DNS, ready to be applied by the networking services when they come up

## During late boot

- In the boot stages that come after the network has been configured, cloud-init runs through the tasks that were not critical for provisioning
- This is where cloud-init configures the running instance according to your needs, as specified in the vendor data and/or user data
- cloud-init will take care of:
	- **Configuration management**
		- cloud-init can interact with tools like Puppet, Ansible, or Chef to apply more complex configuration - and ensure the system is up-to-date
	- **Installing software**
		- Install and run software updates to ensure the system is fully up-to-date and ready to use
	- **User accounts**
		- Create and modify user accounts, set default passwords, and configure permissions
	- **Execute user scripts**
		- If custom scripts were provided in the user data, cloud-init can run them
			- Allows for additional specified software to be installed, security settings to be applied, etc.
			- Can also inject SSH keys into the instance's `authorized_keys` file