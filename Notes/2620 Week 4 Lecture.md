- Logical Link Control (LLC)
	- Used to facilitate multiple upper layer protocols (i.e. network)
- Media access control (MAC)
	- Provides addressing and channel access control mechanisms

- Frames
	-  understand the structure of the frame is important for understanding what is happening at the data link layer
	- the first thing that is read when receiving a frame is the destination address
	- second is the source address
	- payload - in most cases will be an IP packet
	- checksum is applied to the whole frame that is used for detection of corrupted data
		- if checksums don't match, the data is most likely corrupted
	- minimum byte size is 64

- OUI
	- 2^24 available addresses for each OUI
