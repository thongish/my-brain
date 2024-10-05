- spanning-tree protocol
	- enable switches to selectively disable links to avoid circular network traffic
	- 01:80:c2:00:00:00 
		- the address given to spanning tree protocol by IANA

- logical link control tells us the type of payload

- IEEE 802.3 
	- Newest version of ethernet
- Ethernet II (DIX)
	- dec - inter - xerox
	- Most widespread type of ethernet

- These two mean the same thing
	- 255.255.255.0
	- 10.20.30.2/24

- Default gateway is for communicating outside your network not just connecting to the internet
	- no default gateway, there is no way for you to communicate outside your network

# Find IP address

**On PowerShell**
- `Get-NetIPConfiguration`
	- Preferred way to see IP information
	- ipconfig is being deprecated
	- `Get-NetIPAddress` to see information about the IP address alone
- Prefixlength == subnet mask

**On Linux**
- `ifconfig` on Linux
	- being deprecated
- `ip` command is more commonly used now
- `ip route` shows default gateway
- `nmtui` edit IPv4, IPv6, create bridge, etc
- `nmcli` same thing as `nmtui` but command-line based