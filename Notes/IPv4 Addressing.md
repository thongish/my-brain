#NETWORK/W3

# IPv4 address structure

- Address is 32-bits long
- Address broken into four 8-bit segments called octets
	- Each octet is represented by its decimal equivalent value
	- Each octet is separated by a decimal point
	- w.x.y.z notation is used to represent each section of the IPv4 address

# IPv4 classless addressing

- The type of IP addressing currently used
- Network portion of address determined by subnet mask
- Use CIDR notation to show subnet
## CIDR-Based addressing

- Classless Inter-Domain Routing
- Generally starts with 24-bits for the network address prefix and 8 bits for the host ID
	- Looks like w.x.y.z/a where a is the prefix length or number of bits used for the network ID

# Reserved IP addresses and loopback

- Reserved IP addresses are IP addresses set aside by ICANN for specific uses
- Loopback IP addresses are a set of reserved IP addresses that serve a specific function
	- Allow an interface to send a signal back to itself
		- Useful for testing and setting up an interface that is not actually present but can be addressed
	- 127.0.0.1 - 127.255.255.255

# Comparing private, public, and IPv4 APIPA addressing

## Public addressing

- Any interface that needs direct internet access is required to use a public address
- Public addresses need to be registered with ICANN
- Only registered public addresses are allowed direct access to the internet
- If an interface does not need direct access, then a public IP address is not required

## Private addressing

- Only used inside a network that does not directly access the internet
- Certain ranges of IP address are predefined as private addresses by ICANN
- Cannot be used to access internet
- Defined in RFC 1918
	- ICANN will never assign these IP addresses for public use
	- When building private network, use one of the ranged defined as Private IP addresses

## APIPA

- Automatic Private Internet Protocol Addressing
- Created by Microsoft for Windows 9x and higher
- Uses IP address range 169.254.0.0/16
- Uses subnet mask 255.255.0.0
- Used when windows computer is set to automatically find an IP address and DHCP is not available

# Subnetting with IPv4

## What is subnetting?

- Process of breaking a larger network into smaller more manageable networks
	- Each of these smaller networks are called a **subnet**
- Can be done to break up a larger IP address range into smaller address ranges\
- Once broken into smaller rangers, can be used in networks with smaller numbers of computers
	- Prevents wasting IP addresses when using small numbers of computers in a network

## Some basic subnetting rules

- Cannot use first IP address in a range for a computer
	- First IP address in a range is the **network ID**
		- **Network ID** is the address used to identify a specific network to a router
- Cannot use last IP address in a range for a computer
	- Last IP address is the **broadcast address**
		- **Broadcast address** is the IP address that any device on a network would use if they wanted to send a message to all devices on that particular network

# Default routes and gateway settings

## Default routes

- We use default routes because it's not practical to define all possible routes a computer could take to find resources on the internet
- More practical to define one route that summarizes all the locations not on the local subnet
- Summarizing route is what we call the default route
	- Sometimes called **gateway of last resort** because if computer doesn't know where to go, they go to this default route

- Purpose of default route is to offload the responsibility of knowing all possible locations from the local computer to a router
- The IP address of the router that the computer uses to find any addresses or locations  that are outside of the local network is called the default route or the **default gateway**'

## Default gateway setting

- Default gateway provides a destination for the computer to send a packet to that corresponds to all the destinations that are not located on the local network segment the computer is familiar with
- If using DHCP, default gateway is configured on DHCP server and sent automatically
- You can manually configure default gateway

# Understanding and setting a subnet mask

## Subnet mask

- Subnet mask is a special IP address used by the computer to determine what portion of an IP address is intended for the **network ID**, and what portion is intended for the **host ID**
## Subnet mask setting

- Net subnet mask setting is a setting that you put in the network configuration page that tells the computer what subnet mask to use for the particular interface you're trying to configure