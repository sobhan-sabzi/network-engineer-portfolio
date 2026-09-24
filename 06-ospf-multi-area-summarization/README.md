# 06 - OSPF Multi-Area & Route Summarization Lab

## 📌 Overview

This project demonstrates a multi-area OSPF network using Area 0 as the backbone and Area 10 as a separate OSPF area.

R1-ABR acts as the Area Border Router (ABR) between Area 0 and Area 10.

Route summarization is configured on the ABR to advertise the Area 10 networks as a summarized `10.60.0.0/16` route.

## 🛠️ Technologies

- OSPF
- OSPF Multi-Area
- Area 0 Backbone
- Area 10
- Area Border Router (ABR)
- Route Summarization
- Loopback Interfaces
- Passive Interfaces
- Static IP Addressing
- Cisco IOS
- Cisco Packet Tracer

## 🗺️ Network Topology

The topology consists of four routers.

R1-ABR connects OSPF Area 0 to Area 10 and operates as the Area Border Router.

R2 is located in Area 0.

R3 and R4 are located in Area 10.

![Network Topology](./topology.png)

## 🌐 OSPF Areas

### Area 0

Area 0 contains:

- R1-ABR
- R2

Network:

`10.0.12.0/30`

R2 also provides the `10.100.10.0/24` LAN.

### Area 10

Area 10 contains:

- R1-ABR
- R3
- R4

Networks:

- `10.0.13.0/30`
- `10.0.34.0/30`
- `10.60.10.0/24`
- `10.60.20.0/24`

## 🌐 IP Addressing

### R1-ABR

- Gi0/0: `10.0.12.1/30`
- Gi0/1: `10.0.13.1/30`
- Loopback0: `1.1.1.1/32`

### R2

- Gi0/0: `10.0.12.2/30`
- Gi0/1: `10.100.10.1/24`
- Loopback0: `2.2.2.2/32`

### R3

- Gi0/0: `10.0.13.2/30`
- Gi0/1: `10.0.34.1/30`
- Gi0/2: `10.60.10.1/24`
- Loopback0: `3.3.3.3/32`

### R4

- Gi0/0: `10.0.34.2/30`
- Gi0/1: `10.60.20.1/24`
- Loopback0: `4.4.4.4/32`

## 🔄 OSPF Configuration

OSPF process ID:

`20`

### Router IDs

- R1-ABR: `1.1.1.1`
- R2: `2.2.2.2`
- R3: `3.3.3.3`
- R4: `4.4.4.4`

## 🔗 Area Border Router

R1-ABR connects the two OSPF areas.

```text
Area 0 ←→ R1-ABR ←→ Area 10
```

R1-ABR participates in:

- Area 0 through Gi0/0
- Area 10 through Gi0/1

## 📦 Route Summarization

Route summarization is configured on R1-ABR:

```text
area 10 range 10.60.0.0 255.255.0.0
```

The Area 10 networks:

```text
10.60.10.0/24
10.60.20.0/24
```

are summarized as:

```text
10.60.0.0/16
```

This reduces the number of specific routes advertised between OSPF areas.

## 🔒 Passive Interfaces

Passive interfaces are used on LAN-facing interfaces where OSPF neighbor formation is not required.

### R2

```text
GigabitEthernet0/1
```

### R3

```text
GigabitEthernet0/2
```

### R4

```text
GigabitEthernet0/1
```

## 💻 End Devices

Example LANs:

### Area 0

Network:

`10.100.10.0/24`

Example:

```text
PC1
IP: 10.100.10.10
Mask: 255.255.255.0
Gateway: 10.100.10.1
```

### Area 10

Network:

`10.60.10.0/24`

Example:

```text
PC2
IP: 10.60.10.10
Mask: 255.255.255.0
Gateway: 10.60.10.1
```

### Area 10

Network:

`10.60.20.0/24`

Example:

```text
PC3
IP: 10.60.20.10
Mask: 255.255.255.0
Gateway: 10.60.20.1
```

## 🧪 Verification Commands

### OSPF Neighbors

Run on each router:

```text
show ip ospf neighbor
```

### OSPF Interface Status

```text
show ip ospf interface brief
```

### OSPF Database

```text
show ip ospf database
```

### OSPF Routes

```text
show ip route ospf
```

### Full Routing Table

```text
show ip route
```

### OSPF Process

```text
show ip protocols
```

## 🔍 Route Summarization Verification

On R1-ABR:

```text
show ip route
```

The summarized route should be visible as:

```text
10.60.0.0/16
```

On an Area 0 router such as R2:

```text
show ip route ospf
```

The Area 10 networks should be reachable through R1-ABR.

## 📡 Connectivity Tests

From R2:

```text
ping 10.60.10.1
ping 10.60.20.1
ping 3.3.3.3
ping 4.4.4.4
```

From R3:

```text
ping 10.100.10.1
ping 2.2.2.2
```

From R4:

```text
ping 10.100.10.1
ping 1.1.1.1
```

These tests verify end-to-end connectivity between Area 0 and Area 10.

## 📸 Verification Screenshots

### 01 - OSPF Neighbors

![OSPF Neighbors](./screenshots/01-ospf-neighbors.png)

### 02 - OSPF Interfaces

![OSPF Interfaces](./screenshots/02-ospf-interfaces.png)

### 03 - OSPF Routes

![OSPF Routes](./screenshots/03-ospf-routes.png)

### 04 - Route Summarization

![Route Summarization](./screenshots/04-route-summarization.png)

### 05 - OSPF Database

![OSPF Database](./screenshots/05-ospf-database.png)

### 06 - End-to-End Connectivity

![End-to-End Connectivity](./screenshots/06-end-to-end-ping.png)

## 📁 Project Files

- `ospf-multi-area-summarization.pkt` - Cisco Packet Tracer project
- `topology.png` - Network topology
- `screenshots/` - Verification screenshots
- `README.md` - Project documentation

## 🎯 Lab Objective

The objective of this lab is to demonstrate practical knowledge of OSPF multi-area design, Area 0 backbone operation, Area Border Router functionality, route summarization, passive interfaces, and end-to-end routing between different OSPF areas.

## ✅ Verification Summary

- OSPF neighbor relationships verified
- Area 0 adjacency verified
- Area 10 adjacency verified
- ABR functionality verified
- OSPF routes verified
- Route summarization verified
- Passive interfaces verified
- Inter-area connectivity verified
- End-to-end connectivity verified