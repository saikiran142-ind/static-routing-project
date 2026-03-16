# static-routing-project
# 3-Router Static Configuration Project

This project demonstrates a hierarchical network topology using 3 Routers, 3 Switches, and 9 PCs (3 PCs per LAN). The goal is to establish full end-to-end connectivity using **Static Routing**.

## Network Topology Overview
- **Routers:** 3 (R1, R2, R3 connected in a serial chain or mesh)
- **Switches:** 3 (S1, S2, S3 - one per router)
- **End Devices:** 9 PCs (3 per Local Area Network)
- **Routing Protocol:** Static Routing


<img width="1920" height="1080" alt="Screenshot 2026-03-16 202000" src="https://github.com/user-attachments/assets/bfa336df-734c-4bdd-9648-b6ab401a1314" />



## IP Addressing Table

## Complete IP Addressing Table (3 Routers & 9 PCs)

This table outlines the full network configuration, including Local Area Networks (LAN) and Wide Area Network (WAN) Serial links.


| Device | Interface | IP Address | Subnet Mask | Default Gateway | Connected To |
| --- | --- | --- | --- | --- | --- |
| **Router 0** | Gig 0/0/0 | 192.168.60.1 | 255.255.255.0 | N/A | Switch 0 (LAN 1) |
| **Router 0** | Ser 0/1/0 | 10.0.0.1 | 255.255.255.252 | N/A | Router 1 |
| **Router 1** | Gig 0/0/0 | 192.168.70.1 | 255.255.255.0 | N/A | Switch 1 (LAN 2) |
| **Router 1** | Ser 0/1/0 | 10.0.0.2 | 255.255.255.252 | N/A | Router 0 |
| **Router 1** | Ser 0/1/1 | 20.0.0.1 | 255.255.255.252 | N/A | Router 2 |
| **Router 2** | Gig 0/0/0 | 192.168.80.1 | 255.255.255.0 | N/A | Switch 2 (LAN 3) |
| **Router 2** | Ser 0/1/0 | 20.0.0.2 | 255.255.255.252 | N/A | Router 1 |
| **PC 1** | FastEth 0 | 192.168.60.2 | 255.255.255.0 | 192.168.60.1 | Switch 0 |
| **PC 2** | FastEth 0 | 192.168.60.3 | 255.255.255.0 | 192.168.60.1 | Switch 0 |
| **PC 3** | FastEth 0 | 192.168.60.4 | 255.255.255.0 | 192.168.60.1 | Switch 0 |
| **PC 4** | FastEth 0 | 192.168.70.2 | 255.255.255.0 | 192.168.70.1 | Switch 1 |
| **PC 5** | FastEth 0 | 192.168.70.3 | 255.255.255.0 | 192.168.70.1 | Switch 1 |
| **PC 6** | FastEth 0 | 192.168.70.4 | 255.255.255.0 | 192.168.70.1 | Switch 1 |
| **PC 7** | FastEth 0 | 192.168.80.2 | 255.255.255.0 | 192.168.80.1 | Switch 2 |
| **PC 8** | FastEth 0 | 192.168.80.3 | 255.255.255.0 | 192.168.80.1 | Switch 2 |
| **PC 9** | FastEth 0 | 192.168.80.4 | 255.255.255.0 | 192.168.80.1 | Switch 2 |

## Router Configuration 

### Router 0
1. Router> enable
2. Router# configure terminal

! WAN Interface (to Router 1)
1. Router0(config)# interface Serial0/1/0
2. Router0(config-if)# ip address 10.0.0.1 255.0.0.0
3. Router0(config-if)# no shutdown
4. Router0(config-if)# Exit

! LAN Interface
1. Router0(config)# interface GigabitEthernet0/0
2. Router0(config-if)# ip address 192.168.60.1 255.255.255.0
3. Router0(config-if)# no shutdown
4. Router0(config-if)# Exit

### Router 1 Configuration (Middle Router)

1. Router> enable
2. Router# configure terminal

! LAN Interface
1. Router1(config)# interface GigabitEthernet0/0
2. Router1(config-if)# ip address 192.168.70.1 255.255.255.0
3. Router1(config-if)# no shutdown
4. Router1(config-if)# Exit

! WAN Interface (to Router 0)
1. Router1(config)# interface Serial0/1/0
2. Router1(config-if)# ip address 10.0.0.2 255.0.0.0
3. Router1(config-if)# no shutdown
4. Router1(config-if)# Exit

! WAN Interface (to Router 2)
1. Router1(config)# interface Serial0/1/1
2. Router1(config-if)# ip address 20.0.0.1 255.0.0.0
3. Router1(config-if)# no shutdown

### Router 2 Configuration

1. Router> enable
2. Router# configure terminal

! LAN Interface
1. Router2(config)# interface GigabitEthernet0/0
2. Router2(config-if)# ip address 192.168.3.1 255.255.255.0
3. Router2(config-if)# no shutdown
4. Router2(config-if)# Exit

! WAN Interface (to Router 1)
1. Router2(config)# interface Serial0/0/0
2. Router2(config-if)# ip address 10.1.1.6 255.255.255.252
3. Router2(config-if)# no shutdown
4. Router2(config-if)# Exit


## Static Route Configuration
The following commands are manually added to each router to allow communication between different subnets:

### Router 1 (R1)

R1(config)# ip route 192.168.70.0 255.255.255.0 10.0.0.2

R1(config)# ip route 192.168.80.0 255.255.255.0 10.0.0.2

### Router 2
R2(config)# ip route 192.168.60.0 255.255.255.0 10.0.0.1

R2(config)# ip route 192.168.80.0 255.255.255.0 20.0.0.2

### Router 3

R3(config)# ip route 192.168.60.0 255.255.255.0 20.0.0.1

R3(config)# ip route 192.168.70.0 255.255.255.0 20.0.0.1


<img width="920" height="646" alt="image" src="https://github.com/user-attachments/assets/50d60c66-3f54-4f76-8659-0d6374160ae0" />

