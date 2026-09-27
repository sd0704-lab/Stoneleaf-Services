# 01 — Network Design

**Stoneleaf Services**  
*No Stone Left Unturned*

## Purpose

The Network Design phase translates the organizational and technical requirements established in the Stoneleaf Services Foundation into a documented network architecture.

This phase defines how Stoneleaf Services systems will communicate, how network services will be delivered, how traffic will be controlled, and how the environment can expand as additional technical, cybersecurity, investigation, intelligence, and cloud capabilities are introduced.

Network architecture will be designed and documented before implementation.

---

# Objectives

The objectives of the Network Design phase are to:

- Define the logical network architecture.
- Establish an IP addressing strategy.
- Define subnet requirements.
- Determine network segmentation requirements.
- Determine VLAN requirements.
- Define gateway placement.
- Define DHCP architecture.
- Define DNS architecture.
- Define routing requirements.
- Define Network Address Translation (NAT) requirements.
- Define firewall placement and traffic-control requirements.
- Define VMware virtual networking requirements.
- Define connectivity requirements for all core systems.
- Document expected network traffic flows.
- Establish network security boundaries.
- Support centralized identity and authentication.
- Support future security monitoring and logging.
- Support future digital investigation capabilities.
- Support future intelligence and analysis systems.
- Support future Azure and Microsoft Entra integration.
- Provide sufficient documentation for repeatable implementation and troubleshooting.

---

# Design Principles

## Requirements Before Configuration

Network design decisions must be based on documented Stoneleaf Services requirements rather than arbitrary configuration choices.

The design process follows:

**Business Requirement → Technical Requirement → Network Requirement → Design Decision → Implementation → Validation**

---

## Documentation First

The network architecture will be documented before it is deployed.

Design documentation should identify:

- What is being designed
- Why the design is required
- Which systems are affected
- How systems are expected to communicate
- What security boundaries exist
- How the design will be validated
- How the design can expand in the future

---

## Security by Design

Security requirements will be incorporated into the network architecture rather than added after deployment.

The design will consider:

- Network segmentation
- Least privilege
- Firewall enforcement
- Administrative access
- Management traffic
- Server traffic
- User traffic
- Security monitoring
- Logging
- Investigation requirements
- Sensitive organizational functions
- Future cloud connectivity

---

## Separation of Responsibilities

Network services will be assigned deliberately.

The current architectural direction includes:

- **pfSense** — edge firewall, routing, NAT, DHCP, and future VPN functionality
- **Windows Server** — Active Directory Domain Services and internal DNS
- **VMware** — virtual infrastructure and virtual network connectivity
- **Ubuntu Server** — Linux administration and future Linux-based services
- **Windows Workstations** — organizational endpoints representing investigation, intelligence, and management functions

Final configurations will be established through the design process.

---

## Troubleshooting by Design

The network must be designed so that failures can be isolated systematically.

The architecture should support troubleshooting of:

- Physical and virtual connectivity
- IP configuration
- DHCP
- DNS
- Default gateways
- Routing
- NAT
- Firewall rules
- Network segmentation
- Authentication dependencies
- Internet connectivity
- Server connectivity
- Client connectivity
- Cloud connectivity

Network documentation must make normal traffic paths and expected behavior understandable before troubleshooting begins.

---

# Core Network Systems

The initial Stoneleaf Services environment includes the following planned systems:

| Hostname | Platform | Primary Function |
| --- | --- | --- |
| `SLS-FW01` | pfSense | Firewall, routing, DHCP, NAT, and future VPN |
| `SLS-DC01` | Windows Server | Active Directory Domain Services and DNS |
| `SLS-LNX01` | Ubuntu Server 24.04 LTS | Linux administration and services |
| `SLS-WS01` | Windows 11 | Investigations Workstation |
| `SLS-WS02` | Windows 11 | Intelligence / Analysis Workstation |
| `SLS-WS03` | Windows 11 | Management / Administrative Workstation |

These systems represent the initial permanent infrastructure.

Additional systems may be introduced when supported by documented requirements.

---

# Network Design Scope

The Network Design phase will address the following areas.

## Logical Network Architecture

The logical network architecture will define:

- Network boundaries
- Internal networks
- External connectivity
- Firewall placement
- Server connectivity
- Workstation connectivity
- Virtual networking
- Future network segments
- Future cloud connectivity

---

## IP Addressing

An IP addressing plan will define:

- Private address space
- Network addresses
- Subnet masks
- Default gateways
- Static-address ranges
- DHCP ranges
- Reserved addresses
- Infrastructure addresses
- Server addresses
- Client addresses
- Future expansion capacity

The final addressing plan will be documented before implementation.

---

## Network Segmentation

Segmentation requirements will be evaluated based on:

- Security
- Administrative control
- System function
- Traffic isolation
- Sensitive resources
- Monitoring requirements
- Troubleshooting
- Future growth

The number of network segments will be determined during this phase.

---

## VLAN Design

VLAN requirements will be evaluated as part of the segmentation design.

If VLANs are implemented, documentation will define:

- VLAN ID
- VLAN name
- Purpose
- Associated subnet
- Gateway
- DHCP requirements
- Allowed traffic
- Restricted traffic
- Associated systems

VLANs will not be created solely for complexity or portfolio appearance. Each VLAN must have a documented purpose.

---

## DHCP Architecture

pfSense is the planned DHCP service for the initial Stoneleaf Services environment.

The DHCP design will define:

- DHCP scope
- Address pool
- Exclusions
- Reservations
- Lease configuration
- Default gateway
- DNS server assignment
- Domain-related DHCP options where required

Domain-joined systems will ultimately use the appropriate Stoneleaf Services internal DNS service rather than public DNS directly.

---

## DNS Architecture

`SLS-DC01` is planned to provide internal DNS for the Active Directory environment.

The DNS design will define:

- Internal name resolution
- Client DNS configuration
- DNS forwarding
- Active Directory integration
- Internal DNS zones
- External name resolution
- Troubleshooting procedures

The final Active Directory and internal DNS namespace will be selected during the appropriate design stage and will not be assumed prematurely.

---

## Routing

Routing design will determine how traffic moves between networks.

Documentation will identify:

- Connected networks
- Default routes
- Internal routes
- Inter-network routing
- Firewall involvement
- Future cloud routes
- Future VPN routes

Routing decisions must be documented so expected packet paths can be understood and tested.

---

## Network Address Translation

pfSense is planned to perform NAT for appropriate traffic between the Stoneleaf Services private environment and external networks.

The NAT design will document:

- Traffic requiring translation
- Source networks
- Destination networks
- Translation behavior
- Exceptions where required

NAT configuration will be determined after the internal network architecture is finalized.

---

## Firewall Architecture

`SLS-FW01` will serve as the primary firewall for the Stoneleaf Services lab environment.

Firewall design will establish:

- Network interfaces
- Security boundaries
- Allowed traffic
- Restricted traffic
- Administrative access
- Logging requirements
- Inter-network communication
- Internet access
- Future VPN access
- Future cloud connectivity

Firewall rules will follow least-privilege principles.

Rules will be documented before implementation whenever practical.

---

# VMware Network Design

VMware will provide the virtual networking infrastructure required by the Stoneleaf Services virtual environment.

The VMware network design will determine:

- Virtual network types
- Virtual switches or equivalent virtual networking components
- pfSense WAN connectivity
- pfSense LAN connectivity
- Server connectivity
- Workstation connectivity
- Internet access
- Isolation requirements
- Future segmented networks

The VMware network design must support realistic network behavior while remaining practical for a single-host home lab.

Detailed VMware implementation procedures will be maintained in the private Stoneleaf Services runbooks.

---

# Traffic Flow Documentation

Important network traffic flows will be documented.

Examples may include:

- Workstation → DHCP
- Workstation → DNS
- Workstation → Domain Controller
- Workstation → Internet
- Linux Server → Internet
- Administrative Workstation → Server
- Security Monitoring → Managed Systems
- Investigation Workstation → Investigation Resources
- Intelligence Workstation → Intelligence Resources
- Internal Network → pfSense
- pfSense → External Network
- Future On-Premises → Azure
- Future Azure → On-Premises

Traffic-flow documentation should identify:

**Source → Destination → Service/Protocol → Security Control → Expected Result**

---

# Identity and Network Integration

The network architecture must support the Stoneleaf Services identity model established in the Foundation phase.

The environment will eventually support:

- Active Directory authentication
- Centralized DNS
- Domain-joined workstations
- Role-Based Access Control
- Administrative separation
- Security groups
- Group Policy
- Logging
- Security monitoring
- Employee lifecycle exercises

Network architecture should enable these capabilities without making identity architecture dependent on unnecessary network complexity.

---

# Security Monitoring and Logging

The network design must support future centralized security visibility.

Future capabilities may require collection of:

- Firewall logs
- Authentication events
- Windows events
- Linux logs
- DNS activity
- Network connection information
- Security alerts
- Administrative activity

Logging architecture will be developed in a later phase, but the network must not prevent the required systems from communicating with future monitoring infrastructure.

---

# Digital Investigation Support

The network design must support future digital investigation exercises.

Potential requirements include:

- Investigation workstation access
- Evidence-transfer paths
- Logging
- Controlled resource access
- Security-event correlation
- Network activity analysis
- Isolation of systems when required

Detailed investigation architecture will be developed during later Stoneleaf Services phases.

---

# Intelligence and Analysis Support

The network architecture must support future intelligence and analysis capabilities.

Potential requirements include:

- Dedicated workstation access
- Research resources
- Controlled information repositories
- Logging
- Access control
- Future analytical platforms

These capabilities will be introduced only when supported by documented requirements.

---

# Future Azure and Entra Integration

Stoneleaf Services is expected to expand into a hybrid environment using Microsoft Azure and Microsoft Entra ID.

Future network design may include:

- Azure Virtual Network
- Cloud subnets
- Site-to-Site VPN
- Hybrid identity
- Cloud-hosted systems
- Secure on-premises-to-cloud connectivity
- Cloud logging and monitoring
- Cloud security services

Cloud connectivity will be designed after the initial on-premises architecture is established and validated.

---

# Network Documentation

The Network Design phase will produce documentation sufficient to explain and eventually implement the architecture.

Planned documentation may include:

- Network Requirements
- Logical Network Diagram
- IP Addressing Plan
- Subnet Plan
- VLAN Plan
- DHCP Design
- DNS Design
- Routing Design
- NAT Design
- Firewall Architecture
- VMware Network Design
- Traffic Flow Matrix
- Network Security Design
- Future Hybrid Connectivity Plan

Documents will be added as the design develops.

---

# Diagrams

Network diagrams will be maintained as part of the Stoneleaf Services documentation.

Diagrams should clearly identify:

- Systems
- Network boundaries
- Interfaces
- Subnets
- Gateways
- Firewalls
- Servers
- Workstations
- Virtual networking
- Traffic paths
- Future cloud connectivity where applicable

Diagrams must reflect the documented architecture rather than represent unimplemented features as operational.

---

# Validation Planning

Before deployment, the design will define how network functionality will be validated.

Validation may include:

- Client receives expected DHCP configuration
- Client receives correct DNS server
- Client can reach its default gateway
- Internal DNS resolution succeeds
- External DNS resolution succeeds
- Domain Controller is reachable
- Linux Server is reachable as intended
- Workstations communicate only as designed
- Internet connectivity functions
- NAT operates correctly
- Firewall rules allow intended traffic
- Firewall rules block prohibited traffic
- Network segments communicate only where authorized
- Logs are generated where required

Exact validation procedures will be developed alongside the final design.

---

# Troubleshooting Documentation

Network troubleshooting documentation will follow the Stoneleaf Services troubleshooting methodology.

Troubleshooting should progress systematically through relevant layers and services rather than assuming a failed component.

Potential troubleshooting tools include:

- `ipconfig`
- `ping`
- `tracert`
- `nslookup`
- `route`
- `arp`
- `netstat`
- PowerShell networking commands
- Linux networking utilities
- pfSense diagnostics
- Wireshark

Troubleshooting exercises will later be documented in:

`09-Troubleshooting-Labs`

---

# Change Management

Significant network changes will follow the Stoneleaf Services change-management process.

Examples include:

- Changing IP addressing
- Creating or modifying network segments
- Creating VLANs
- Changing DHCP scopes
- Changing DNS configuration
- Modifying routes
- Changing NAT
- Modifying firewall rules
- Changing VMware virtual networks
- Changing gateway configuration
- Introducing cloud connectivity

Changes should include implementation, validation, rollback, and final-state documentation where appropriate.

---

# Current Status

**Phase:** Network Design  
**Status:** Planning / Design  
**Deployment Status:** Not Started

The Foundation phase has established the organizational, technical, identity, documentation, inventory, naming, and change-management requirements necessary to begin network architecture.

The current phase focuses on designing the network before technical deployment.

Deployment will remain deferred until sufficient local storage is available for the planned virtual environment.

---

# Design Sequence

The initial Network Design process will proceed in the following general order:

1. Review Foundation requirements.
2. Identify network requirements.
3. Define the logical network topology.
4. Establish the IP addressing strategy.
5. Determine subnet requirements.
6. Determine segmentation requirements.
7. Determine VLAN requirements.
8. Define gateway architecture.
9. Design DHCP.
10. Design DNS.
11. Design routing.
12. Design NAT.
13. Design firewall architecture.
14. Design VMware virtual networking.
15. Document major traffic flows.
16. Develop the logical network diagram.
17. Define validation requirements.
18. Review the design for security, scalability, and troubleshooting.
19. Finalize Network Design documentation.
20. Prepare for the VMware implementation phase.

---

# Completion Criteria

The Network Design phase will be considered complete when:

- Network requirements are documented.
- Logical topology is defined.
- IP addressing is defined.
- Subnets are defined.
- Segmentation decisions are documented.
- VLAN decisions are documented.
- DHCP architecture is defined.
- DNS architecture is defined.
- Routing architecture is defined.
- NAT requirements are defined.
- Firewall architecture is defined.
- VMware virtual networking is defined.
- Major traffic flows are documented.
- Network diagrams are complete.
- Validation requirements are documented.
- Security considerations have been reviewed.
- Future expansion has been considered.
- Documentation accurately reflects the intended architecture.

Once these criteria are satisfied, Stoneleaf Services can proceed to the VMware implementation phase.

---

# Next Phase

After Network Design is completed, development proceeds to:

`02-VMware`

The VMware phase will translate the approved network and infrastructure design into the virtual environment required to host the Stoneleaf Services systems.

Detailed implementation will be documented through the Stoneleaf Services private runbook system.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
