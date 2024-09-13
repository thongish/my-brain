# Hub and spoke

- Remote sites connect back to a central hub
- Minimizes number of WAN links
	- Cheaper to set up
- Can result in suboptimal paths
	- ex. Remote site 1 wants to talk to remote site 2 but the data has to travel from site 1 to the central hub, then to site 2

# Full mesh

- Connecting every site to every other site
- Results in optimal pathing because there is a direct link between any two sites
- Very expensive
- Not scalable
- (n(n-1))/2 = # of links, where n is the number of sites

# Partial mesh

- A subset of a full mesh topology
- Links are strategically added based on traffic patterns
	- If one site is frequently talking to another site, add a link 

# Ring

- Interconnects devices in a circular fashion
- Not widely used in modern networks
- Logical topology is that all devices are connected in a ring
- In reality, physical topology, all devices are connected to a **Media Access Unit** (MAU)
- Data moves from device to device until it reaches where it's supposed to go

# Bus

- Devices are connected to the same coaxial cable

# Star

- Devices connect back to a centralized device (router, switch)
- If one link fails, other links continue to function
- Centralized device is a single point of failure

# Point-to-Point

- Interconnecting two devices
- Typically uses a Layer 2 protocol
	- Point-to-Point protocol (PPP)
	- High-Level data Link Control (HDLC)
- Could be a physical point-to-point connection
- Could be a logical point-to-point connection

# Point-to-Multipoint

- A WAN connection where one location connects, via a single physical location, to multiple locations
- Could be considered a hub and spoke topology

# Hybrid

- A network topology containing elements of multiple types of network topologies