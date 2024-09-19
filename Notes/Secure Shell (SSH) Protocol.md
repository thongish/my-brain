#LINUX/W1
# What is SSH?

- A method for securely sending commands to a computer over an unsecured network
- Uses cryptography to authenticate and encrypt connections between devices
- Also allows for **tunneling**, or port forwarding which is when data packets are able to cross networks that they would not otherwise be able to cross
- Often used for controlling servers remotely 

# What does SSH do?

## Remote encrypted connections

- Sets up connection between a user's device and a faraway machine, often a server
- Uses encryption methods that make decryption very difficult for outsiders
## Ability to tunnel

- Tunneling is a method for moving packets across a network using a protocol or path they would not normally be able to use
- Works by wrapping data packets with additional information called **headers** to change their destination
- SSH Tunnels use port forwarding to send packets from one machine to another

# How does SSH work?

## TCP/IP

- SSH runs on top of the **TCP/IP** protocol
	- **Transmission Control Protocol** and **Internet Protocol**
	- IP indicates which IP address a packet should go while TCP indicates which port a packet should go to at each IP address
	- TCP is a transport layer protocol and is concerned with the transportation and delivery of data packets
	- Additional protocols are used on top of TCP/IP in order to put the transmitted data  in a form that applications can use
		- Such as SSH

## Public key cryptography

- Public key cryptography is a way to encrypt data, or sign data, with two different keys
	- One of the keys, the **public key**, is available to anyone to use
	- The other key, the **private key** is kept secret by its owner
- In an SSH connection, both sides have a public/private key pair, and each side authenticates the other using these keys

## Authentication

- While public key cryptography authenticates the connected devices in SSH, a properly secured computer will still require authentication from the person using SSH
	- Often takes form of entering a username and password

# What is SSH used for?

- Remotely managing servers, infrastructure, and employee computers
- Securely transferring files (SSH is more secure than unencrypted protocols like FTP)
- Accessing services in the cloud without exposing a local machine's ports to the internet
- Connecting remotely to services in a private network
- Bypassing firewall restrictions

# What port does SSH use?

- Port 22 is the default port for SSH



# Flash cards

What is SSH?::A method for securely sending commands to a computer over an unsecured network.
<!--SR:!2024-09-20,1,212-->

What is public key cryptography?::A method to encrypt or sign data with two different keys: a public key available to anyone and a private key kept secret by its owner.
<!--SR:!2024-09-20,1,212-->

How does SSH use public key cryptography?::Both sides in an SSH connection have a public/private key pair and authenticate each other using these keys.
<!--SR:!2024-09-20,1,212-->

What additional authentication is often required in SSH?::A username and password.
<!--SR:!2024-09-22,3,252-->

What is SSH used for?
?
- Remotely managing servers, 
- securely transferring files, 
- accessing cloud services, 
- connecting to private network services,
- and bypassing firewall restrictions.
<!--SR:!2024-09-20,1,212-->

What port does SSH use?::Port 22.
<!--SR:!2024-09-22,4,270-->