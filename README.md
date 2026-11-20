# Multi-Branch Transport Office Network (Sana'a & Dhamar)

Design and implementation of an enterprise network for a transport office with two branches, Sana'a and Dhamar, built in Cisco Packet Tracer. The project connects both branches through routers, uses a mesh topology for redundancy, segments each branch into VLANs managed with VTP, enables Inter-VLAN routing, automates addressing with DHCP, and links the branches using a dynamic routing protocol.

---

##  Overview

The transport office operates from two locations. Each branch has three departments with different roles, so the network separates them logically for security and performance while still allowing controlled communication between them. Redundant links keep the network running even if one connection fails.

##  Key Features

- **Two-branch connectivity:** Sana'a and Dhamar are linked through their routers.
- **Mesh topology:** switches are interconnected with redundant paths, so communication continues if a link fails.
- **VLAN segmentation:** each branch is divided into three VLANs by department.
- **VTP:** VLAN information is configured once and propagated to the other switches.
- **Inter-VLAN routing:** allows departments to communicate with each other through the router.
- **DHCP:** IP addresses are distributed automatically to all devices.
- **Dynamic routing:** a routing protocol exchanges routes between the two branches automatically.
- **Loop prevention:** Spanning Tree Protocol (STP) blocks redundant links to avoid switching loops and reactivates them when needed.

##  Network Topology

Each branch uses the same design:

| Component | Details |
|---|---|
| Router | Cisco 2911 (Router1 for one branch, Router2 for the other) |
| Switches | 3 × Cisco 2960-24TT per branch, connected in a mesh |
| End devices | PCs distributed across the three departments |

| | Branch 1 [Sana'a] | Branch 2 [Dhamar] |
|---|---|---|
| Router | Router1 | Router2 |
| Main switch | Switch1 | Switch7 |
| Sales switch | Switch2 | Switch6 |
| Operations switch | Switch3 | Switch8 |


##  VLAN Design

| VLAN ID | Department | Devices (Branch 1) | Devices (Branch 2) |
|---|---|---|---|
| 10 | Administration | PC1, PC8, PC9 | PC4, PC14, PC15 |
| 20 | Reservations & Sales | PC0, PC6, PC7 | PC3, PC12, PC13 |
| 30 | Operations (Movement) | PC2, PC10, PC11 | PC5, PC16, PC17 |

##  Mesh Topology and Redundancy

The switches in each branch are connected to each other through multiple links instead of a single path. If one link or switch fails, traffic automatically takes an alternative path. **STP** prevents loops by keeping one redundant link blocked (shown with an orange indicator in Packet Tracer) and activating it on failure.

##  Protocols and Technologies

| Technology | Purpose |
|---|---|
| VLAN | Logical separation of departments |
| VTP | Centralized VLAN management and propagation |
| Trunking (802.1Q) | Carries multiple VLANs over switch links |
| Inter-VLAN Routing | Communication between departments |
| DHCP | Automatic IP address assignment |
| STP | Loop prevention in the mesh topology |
| [ RIP ] | Dynamic routing between the two branches |

##  IP Addressing Plan


| Branch | VLAN | Network | Gateway |
|---|---|---|---|
| Sana'a | 10 | [192.168.10.0/24] | [192.168.10.1] |
| Sana'a | 20 | [192.168.20.0/24] | [192.168.20.1] |
| Sana'a | 30 | [192.168.30.0/24] | [192.168.30.1] |
| Dhamar | 10 | [192.168.110.0/24] | [192.168.110.1] |
| Dhamar | 20 | [192.168.120.0/24] | [192.168.120.1] |
| Dhamar | 30 | [192.168.130.0/24] | [192.168.130.1] |
| Router link | | [10.0.0.0/30] | |

##  Verification

After opening the project, you can verify that everything works:

1. **DHCP:** open any PC, then **Desktop**, then **IP Configuration**, and confirm it received an address.
2. **Same VLAN:** ping a PC in the same department.
3. **Inter-VLAN:** ping a PC in a different department.
4. **Between branches:** ping a PC in the other branch.
5. **Redundancy:** disconnect one link between switches and confirm connectivity remains.
6. **Commands:** use `show vlan brief`, `show vtp status`, `show ip route`, and `show spanning-tree` on the devices.

##  How to Run

1. Install **Cisco Packet Tracer** [ 8.2.1 64Bit ].
2. Download the project file ` Transport Office Network.pkt ` from this repository.
3. Open it and wait until the links turn green.
4. Test connectivity using the steps above.

##  Repository Structure

```
├── Transport Office Network.pkt       # Packet Tracer project file
├── Images/
│   └── Topology.png             # Network topology
└── README.md
```

##  Skills Demonstrated

- Enterprise network design for multiple branches
- VLAN segmentation and VTP configuration
- Redundant (mesh) topology and Spanning Tree
- Inter-VLAN routing and DHCP services
- Dynamic routing between remote sites
