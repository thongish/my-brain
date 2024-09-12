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

## Physical layer

- Responsible for, 
	- How bits are represented on the medium (cables, Wi-Fi)
	- Wiring standards for connectors and jacks
	- Physical topology
	- Synchronizing bits
	- Bandwidth usage
	- Multiplexing strategy
		- How to send more than one conversation on a single medium

## Data Link layer

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
