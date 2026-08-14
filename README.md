# Secure Network Restructuring Using GNS3 and pfSense

## Project Overview

This project demonstrates how I restructured and secured a simulated organizational network in GNS3. I separated the Customer Experience, Human Resources, and server networks using VLANs. I also configured pfSense firewall rules to allow inbound HTTP and HTTPS traffic only to the designated WebServer.

> This project was completed in a simulated lab environment for educational and portfolio purposes.
> ## Network Topology

The following diagram shows the completed organizational network in GNS3.

![Completed GNS3 network topology](Screenshot%202026-08-13%20201631.png)

## Configuration Evidence

### BackboneSwitch — VLAN 1

The backbone switch connects the firewall and routers through the central network infrastructure.

![BackboneSwitch VLAN 1 configuration](Screenshot%202026-08-13%20201720.png)

### Customer Experience — VLAN 2

CustExpSwitch ports 0 through 6 were configured as access ports in VLAN 2.

![Customer Experience VLAN 2 configuration](Screenshot%202026-08-13%20201750.png)

### Human Resources — VLAN 3

HRSwitch ports 0 through 3 were configured as access ports in VLAN 3.

![Human Resources VLAN 3 configuration](Screenshot%202026-08-13%20201811.png)

### Server Network — VLAN 4

ServerSwitch ports 0 through 2 were configured as access ports in VLAN 4.

![Server network VLAN 4 configuration](Screenshot%202026-08-13%20201832.png)

### pfSense WAN Firewall Rules

The firewall allows HTTP and HTTPS traffic to the designated WebServer and blocks those services from reaching other internal systems.

![pfSense WAN firewall rules](Screenshot%202026-08-13%20201857.png)

## Objectives

- Build an organized departmental network topology
- Separate departments and servers using VLANs
- Reduce unauthorized communication between networks
- Configure inbound HTTP and HTTPS firewall rules
- Apply least privilege and network segmentation
- Support confidentiality, integrity, and availability

## Tools Used

- GNS3
- pfSense
- Virtual Ethernet switches
- Virtual routers, servers, and endpoint computers
- Microsoft Word for technical documentation

## Network Configuration

| Network | Switch | Ports | VLAN |
|---|---|---:|---:|
| Backbone Infrastructure | BackboneSwitch | Active backbone ports | 1 |
| Customer Experience | CustExpSwitch | 0–6 | 2 |
| Human Resources | HRSwitch | 0–3 | 3 |
| Server Network | ServerSwitch | 0–2 | 4 |

## Firewall Rules

| Order | Action | Protocol | Destination | Port |
|---:|---|---|---|---|
| 1 | Allow | TCP | WebServer 192.168.4.2 | 80 |
| 2 | Allow | TCP | WebServer 192.168.4.2 | 443 |
| 3 | Block | TCP | All other internal systems | 80 |
| 4 | Block | TCP | All other internal systems | 443 |

The allow rules were placed above the block rules because pfSense evaluates firewall rules from top to bottom and applies the first matching rule.

## Security Benefits

- VLAN segmentation separates departmental and server traffic.
- Network separation helps limit lateral movement.
- Only the WebServer is exposed on ports 80 and 443.
- Employee computers and the AuthServer are protected from unnecessary inbound traffic.
- Traffic passing between separated networks can be controlled and monitored.

## CIA Triad

- **Confidentiality:** VLAN separation limits unnecessary access to sensitive HR and authentication traffic.
- **Integrity:** Segmentation and firewall rules reduce opportunities for unauthorized changes.
- **Availability:** A problem in one VLAN is less likely to affect the entire organization, helping maintain access to critical network services.

## Challenges and Lessons Learned

During this project, I encountered switch-port assignment and pfSense access issues. I reviewed the topology, verified the VLAN assignments, checked the firewall rule order, and compared the completed configuration with the project requirements.

This project helped me understand how VLANs, routing, firewall rules, and network segmentation work together to protect an organizational network.
