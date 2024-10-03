#NETWORK/W1
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


# Flash cards

What is a hub and spoke topology?::Remote sites connect back to a central hub, minimizing the number of WAN links, making it cheaper to set up but can result in suboptimal paths.
<!--SR:!2024-10-06,4,210-->

What is a drawback of the hub and spoke topology?::Data may travel through the central hub even when two remote sites need to communicate directly, leading to suboptimal paths
<!--SR:!2024-10-14,12,230-->

What is a full mesh topology?::A topology where every node is connected to every other node, resulting in optimal pathing, but is very expensive and not scalable.
<!--SR:!2024-10-05,8,250-->

How do you calculate the number of links in a full mesh topology?::Use the formula (n(n-1))/2, where n is the number of sites.
<!--SR:!2024-10-14,12,230-->

What is a partial mesh topology?::A subset of a full mesh topology, where links are added based on traffic patterns between frequently communicating sites.
<!--SR:!2024-10-03,1,190-->

What is a ring topology?::A topology where devices are interconnected in a circular fashion, with data traveling from device to device until it reaches its destination.
<!--SR:!2024-10-14,12,230-->

What is a bus topology?::Devices are connected to the same coaxial cable.
<!--SR:!2024-10-14,12,230-->

What is a star topology?::Devices connect back to a centralized device (like a router or switch), where failure of one link doesn't affect others, but the central device is a single point of failure.
<!--SR:!2024-10-14,12,230-->

What is a point-to-point connection?::A topology interconnecting two devices, often using Layer 2 protocols like PPP or HDLC, and can be a physical or logical connection.
<!--SR:!2024-10-03,1,170-->

What is a point-to-multipoint connection?::A WAN connection where one location connects to multiple locations via a single physical connection, often considered a hub and spoke topology.
<!--SR:!2024-10-03,1,170-->

What is a hybrid topology?::A network topology that contains elements of multiple types of network topologies.
<!--SR:!2024-10-08,6,230-->