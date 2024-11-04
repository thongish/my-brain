# Variable length subnetting

## 192.168.15.0/24

Requirements: 3 subnets
- 50 hosts
- 100 hosts
- 40 hosts

Before beginning subnetting determine whether the requirements are possible within the original range

- 50 hosts + 2 = 52 => 64
- 100 hosts + 2 = 102 => 128
- 40 hosts + 4 = 42 => 64
- total = 256

Find the nearest power of 2 to the number of hosts + 2 and add them together and figure out if it fits within the range of the prefix range, in this case 24

Sort the subnets by largest to smallest

- 100 hosts + 2 = 102 => 128
- 50 hosts + 2 = 52 => 64
- 40 hosts + 4 = 42 => 64



192.168.15.0 - 192.168.15.127/ -> subnet 1 -> prefix 25
192.168.15.128 - 192.168.15.191 -> subnet 2 -> prefix 26
192.168.15.192 - 192.168.16.255 -> subnet 3 -> prefix 26

## 10.20.30.0/24

Requirements: 5 subnets
- 10 hosts
- 20 hosts
- 100 hosts
- 40 hosts
- 8 hosts

## 10.0.29.128/25

Requirements:
- 20 hosts + 2 = 22 -> 32
- 16 hosts + 2 = 18 -> 32
- 30 hosts + 2 = 32 -> 32
- 25 hosts + 2 = 27 -> 32

10.0.29.128 - 10.0.29. 159/27
10.0.29.160 - 10.0.29.191/27
10.0.29.192 - 10.0.29. 223/27
10.0.29.224 - 10.0.29.255/27

# Supernetting

- Works in reverse direction in relation to subnetting
- Route aggregation: subnets that share the same prefix are aggregated into alarger network
- Useful for reducing the number of entries in routing tables which increases routing efficiency


