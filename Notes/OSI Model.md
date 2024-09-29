#NETWORK/W1
# Open systems interconnect Model

- Contains 7 different layers
- International Standards Organization (ISO)
	- The ISO defined the OSI Model
# Terminology

**Protocol Data Units** (PDUs)
- The names given to data at different layers of the OSI Model
## 7 Layers bottom to top

1. Physical 
	1. PDU = bits
2. Data Link
	1. PDU = Frames, Packets
3. Network
	1. PDU = Packets, Datagrams
4. Transport
	1. PDU = Segments, Packets
5. Session
6. Presentation
7. Application

- **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way
	- To remember the 7 layers from bottom to top layer

# Physical layer

- Responsible for, 
	- How bits are represented on the medium (cables, Wi-Fi)
	- Wiring standards for connectors and jacks
	- Physical topology
	- Synchronizing bits
	- Bandwidth usage
	- Multiplexing strategy
		- How to send more than one conversation on a single medium

# Data Link layer

### Two sub-layers

1. **Logical Link Control**
	- Connection services
		- Flow Control
			- Allows a receiver to tell the sender to slow down its transmission rate
		- Error Control
			- Allows a receiver to detect an error in a received frame, and request the sender to retransmit
	- Synchronizing transmissions

2. **Media Access Control**
	- Physical addressing
	- Logical topology
		- How traffic logically flows between devices
	- Method of transmitting on the media

# Network layer

- Responsible for,
	- Logical addressing (IPv4, IPv6)
	- Switching
		- **Packet switching**
			- A data stream is divided into packets
			- Packet contains a header with a source and destination address
		- **Circuit switching**
			- A temporary connection that is brought up on an as-needed basis
				- Similar to a phone call
		- **Message switching** 
			- A data stream is broken into messages which are not necessarily delivered immediately
			- Uses a store-and-forward approach, similar to e-mail
	- Route discovery and selection
	- Connection services
		- Flower control
		- Packet reordering

# Transport layer

- 3 main concerns
	- **Protocols**
		- Transmission Control Protocol (TCP)
			- Reliable
			- Send data, receive acknowledgement from destination that data has been received
		- Internet Protocol (IP) ??
		- User Datagram Protocol (UDP)
			- Unreliable
			- Often called a connectionless protocol (no acknowledgement)
			- Has significantly lower overhead than TCP
	- **Windowing**
		- Sliding window
			- Allows TCP window size (i.e. number of segments that can be sent before an acknowledgement is received) to grow, based on network reliability
			- Incremental increase of window size 
	- **Buffering**
		- Queue (buffer)
			- Memory used by a router's output interface to store packets until bandwidth becomes available to transmit those packets

# Session

- Responsible for,
	- Setting up a session
	- Maintaining a session
	- Tearing down a session

# Presentation

- Responsible for,
	- Data formatting
	- Encryption

# Application

- Concerned with,
	- Application services
		- Services that support applications
		- i.e. Email service to support Microsoft Outlook
	- Service advertisement
		- Make network resource known to devices on the network
			- i.e. A shared printer


# Flash cards

What is a **Protocol Data Unit**?::The names given to data at different layers of the OSI Model
<!--SR:!2024-10-02,5,230-->

What mnemonic device is used to remember the 7 OSI Model layers from bottom to top?::**P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way
<!--SR:!2024-09-28,1,190-->

What is the **Protocol Data Unit** at the Physical layer of the OSI Model?::Bits
<!--SR:!2024-10-05,8,250-->

What is the **Protocol Data Unit** at the Data Link layer of the OSI Model?::Frames (sometimes packets)
<!--SR:!2024-09-28,1,190-->

What is the **Protocol Data Unit** at the Network layer of the OSI Model?::Packets (sometimes datagrams)
<!--SR:!2024-10-02,5,230-->

What is the **Protocol Data Unit** at the Transport layer of the OSI Model?::Segments or Datagrams
<!--SR:!2024-09-29,2,210-->

What is the main responsibility of the Physical Layer?
?
Responsible for:
- how bits are represented on the medium, 
- wiring standards, 
- physical topology, 
- bit synchronization, 
- bandwidth usage, 
- and multiplexing strategies
<!--SR:!2024-09-28,1,190-->

What does **multiplexing** in the Physical Layer refer to?::It refers to the strategy of sending more than one conversation on a single medium
<!--SR:!2024-09-29,2,210-->

What are the two sub-layers of the **Data Link** Layer?::Logical Link Control (LLC) and Media Access Control (MAC)
<!--SR:!2024-10-02,5,230-->

What are the key functions of the **Network Layer**?
?
- Logical addressing (IPv4, IPv6),
- switching (packet, circuit, and message switching), 
- route discovery and selection,
- and connection services like:
	- flow control 
	- and packet reordering.
<!--SR:!2024-09-28,1,190-->

What is packet switching?::Dividing a data stream into packets, where each packet has a header with source and destination addresses, before sending it off
<!--SR:!2024-09-28,1,190-->

What is circuit switching?::A temporary connection set up on an as-needed basis, similar to a phone call.
<!--SR:!2024-09-28,1,190-->

What is message switching?::Breaking a data stream into messages, which are stored and forwarded, not necessarily delivered immediately (like email).
<!--SR:!2024-09-28,1,190-->

What are the three main concerns of the **Transport** Layer?::Protocols, windowing, and buffering.
<!--SR:!2024-09-29,2,210-->

What is **windowing** in TCP?::The process where the TCP window size grows based on network reliability, allowing more segments to be sent before an acknowledgment is received.
<!--SR:!2024-09-28,1,190-->

What is **buffering** in the Transport Layer?::The use of memory (a buffer or queue) by a router to store packets until bandwidth is available for transmission.
<!--SR:!2024-09-29,2,210-->

What are the responsibilities of the **Session Layer**?::Setting up, maintaining, and tearing down a session.
<!--SR:!2024-10-02,5,230-->

What is the main responsibility of the **Presentation Layer**?::Data formatting and encryption.
<!--SR:!2024-09-29,2,210-->