# Stoneleaf Services — Network Requirements

**No Stone Left Unturned**

## Purpose

This document defines the network requirements for the Stoneleaf Services technical environment.

The requirements established here translate the organizational, business, technical, identity, security, investigation, and future cloud requirements defined during the Foundation phase into specific networking capabilities.

This document defines **what the network must support**.

It does not define the final network architecture.

Specific design decisions including IP address ranges, subnet boundaries, VLAN IDs, firewall rules, VMware virtual networks, and routing configurations will be established in subsequent Network Design documents.

---

# Requirements Development Model

Stoneleaf Services uses the following design progression:

**Business Requirement → Technical Requirement → Network Requirement → Design Decision → Implementation → Validation**

Network requirements therefore establish capabilities before specific technologies or configurations are selected.

---

# Network Environment

The initial Stoneleaf Services environment will operate as a virtualized organizational network hosted primarily through VMware.

The initial permanent systems are:

| Hostname | Platform | Primary Function |
| --- | --- | --- |
| `SLS-FW01` | pfSense | Firewall, routing, DHCP, NAT, and future VPN |
| `SLS-DC01` | Windows Server | Active Directory Domain Services and DNS |
| `SLS-LNX01` | Ubuntu Server 24.04 LTS | Linux administration and services |
| `SLS-WS01` | Windows 11 | Investigations Workstation |
| `SLS-WS02` | Windows 11 | Intelligence / Analysis Workstation |
| `SLS-WS03` | Windows 11 | Management / Administrative Workstation |

The network must support these systems while allowing additional infrastructure to be introduced as Stoneleaf Services develops.

---

# Network Requirements

## NR-01 — Private Network Infrastructure

Stoneleaf Services must provide a private internal network for lab systems.

The internal environment must use private IP addressing and must not expose internal systems directly to external networks unless specifically required and securely configured.

---

## NR-02 — Central Network Boundary

The environment must provide a defined network boundary between the Stoneleaf Services internal network and external networks.

Traffic crossing this boundary must be subject to routing, firewall, and other applicable security controls.

---

## NR-03 — Firewall Capability

The network must provide stateful firewall capabilities capable of controlling traffic between network boundaries.

Firewall functionality must support:

- Inbound traffic control
- Outbound traffic control
- Inter-network traffic control
- Administrative access restrictions
- Traffic logging
- Future network segmentation
- Future VPN connectivity

`SLS-FW01` is the planned firewall platform.

---

## NR-04 — Routing Capability

The network must support routing between networks when multiple network segments are introduced.

Routing must provide controlled communication between authorized networks while allowing firewall policy to restrict unauthorized communication.

---

## NR-05 — Network Address Translation

The network must support Network Address Translation where required for communication between private Stoneleaf Services networks and external networks.

NAT must allow internal systems to access appropriate external resources without requiring publicly routable addresses for internal systems.

---

## NR-06 — Dynamic Host Configuration

The environment must provide DHCP services for systems that do not require manually assigned addresses.

DHCP must be capable of distributing appropriate:

- IP addresses
- Subnet information
- Default gateway information
- DNS server information
- Lease information
- Other required network configuration

pfSense is the planned DHCP platform for the initial environment.

---

## NR-07 — Static Infrastructure Addressing

Critical network infrastructure and server systems must support predictable addressing.

Systems requiring stable network locations may include:

- Firewalls
- Domain controllers
- DNS servers
- Servers
- Network infrastructure
- Logging systems
- Monitoring systems
- Future storage infrastructure

The specific static-address ranges will be defined in the IP Addressing Plan.

---

## NR-08 — Internal DNS

The network must provide internal DNS services capable of supporting the Stoneleaf Services Windows domain environment.

Internal DNS must support:

- Active Directory
- Internal hostname resolution
- Domain-joined systems
- Internal services
- External DNS resolution through appropriate forwarding or resolution mechanisms

`SLS-DC01` is planned to provide Active Directory-integrated internal DNS.

---

## NR-09 — Correct Client DNS Assignment

Domain-joined systems must use the appropriate Stoneleaf Services internal DNS service.

Domain clients must not depend directly on public DNS servers for Active Directory-related name resolution.

DHCP and static network configuration must support correct DNS assignment.

---

## NR-10 — Internet Connectivity

Authorized Stoneleaf Services systems must be capable of accessing external network and internet resources where required.

External access may be required for:

- Operating-system updates
- Software installation
- Package repositories
- Vendor resources
- Cloud services
- Security updates
- Research
- Administrative functions

Internet connectivity must pass through the appropriate network security boundary.

---

## NR-11 — Network Segmentation Capability

The network architecture must support segmentation.

Segmentation may be used to separate systems based on:

- Security requirements
- Administrative function
- System role
- User function
- Sensitive information
- Server infrastructure
- Management traffic
- Security operations
- Investigations
- Intelligence activities
- Future guest or testing environments
- Future cloud connectivity

The number and purpose of network segments will be determined during the segmentation design process.

---

## NR-12 — VLAN Capability

The network architecture must support VLAN-based segmentation if VLANs are determined to be appropriate.

VLANs must be created only when they provide a documented technical, security, administrative, or operational benefit.

Specific VLAN IDs, names, subnets, and associated systems will be defined later.

---

## NR-13 — Controlled Inter-Segment Communication

If multiple network segments are implemented, communication between segments must be controllable.

Inter-segment traffic must be capable of being:

- Allowed
- Restricted
- Logged
- Monitored
- Troubleshot

Access should follow least-privilege principles.

---

## NR-14 — VMware Virtual Networking

The network must operate within the VMware virtualization environment used by Stoneleaf Services.

VMware networking must support:

- pfSense connectivity
- Internal network connectivity
- Server connectivity
- Workstation connectivity
- Internet access
- Network isolation
- Future segmentation
- Future additional virtual systems

The final VMware virtual network architecture will be documented separately.

---

## NR-15 — Firewall Interface Expansion

The network architecture must allow `SLS-FW01` to support multiple network interfaces if required by the final segmentation architecture.

Interfaces may represent:

- External connectivity
- Internal networks
- Management networks
- Server networks
- Security zones
- Other future network segments

Final interface assignments will be determined during design.

---

## NR-16 — Active Directory Connectivity

The network must support reliable communication between domain-joined systems and `SLS-DC01`.

The network must support services required for:

- Authentication
- Active Directory
- DNS
- Group Policy
- Domain joining
- Identity management
- Administrative functions

Required network flows will be documented in the Traffic Flow Matrix.

---

## NR-17 — Windows Client Connectivity

The network must support the planned Stoneleaf Services Windows workstations:

- `SLS-WS01`
- `SLS-WS02`
- `SLS-WS03`

Workstations must be capable of reaching authorized:

- Infrastructure services
- Domain services
- DNS services
- Internet resources
- Future application services
- Future monitoring systems

Access to other resources must depend on organizational and security requirements.

---

## NR-18 — Linux Server Connectivity

The network must support `SLS-LNX01`.

The Ubuntu Server must be capable of receiving appropriate:

- IP configuration
- DNS resolution
- Administrative access
- Internet access
- Software updates
- Future internal service connectivity

Access to the server must be controllable and monitorable.

---

## NR-19 — Administrative Connectivity

Authorized administrators must be capable of securely managing Stoneleaf Services infrastructure.

Administrative network access may include:

- pfSense administration
- Windows Server administration
- Active Directory administration
- Linux administration
- VMware administration
- Future cloud administration
- Future security-platform administration

Administrative access must follow least-privilege principles.

---

## NR-20 — Role Separation Support

The network architecture must support the organizational separation established by the Stoneleaf Services Identity Roster.

The network must be capable of supporting different access requirements for:

- Executive Leadership
- Information Technology
- Cybersecurity
- Digital Investigations
- Intelligence & Analysis
- Business Operations
- Project & Client Services
- Legal & Compliance

Network segmentation will not automatically mirror organizational departments.

Segmentation decisions must be based on technical and security requirements.

---

## NR-21 — Security Monitoring Support

The network must support future centralized security monitoring.

Future monitoring systems may require access to:

- Firewall logs
- Windows logs
- Linux logs
- Authentication events
- DNS activity
- Network events
- Security alerts
- Endpoint telemetry

The network must permit required monitoring traffic while protecting monitoring infrastructure from unnecessary access.

---

## NR-22 — Network Logging

Network infrastructure must support logging appropriate events.

Potential events include:

- Firewall activity
- Blocked connections
- Allowed connections where appropriate
- Administrative activity
- VPN activity
- DHCP events
- DNS events
- Security events

Logging requirements will be refined during later security and monitoring phases.

---

## NR-23 — Troubleshooting Capability

The network must support systematic troubleshooting.

Administrators must be capable of testing:

- Local interface configuration
- IP addressing
- Local connectivity
- Default gateway connectivity
- DNS resolution
- Internal routing
- External routing
- NAT
- Firewall behavior
- Server connectivity
- Client connectivity
- Internet connectivity

Network design must avoid unnecessary complexity that makes troubleshooting more difficult without providing a corresponding benefit.

---

## NR-24 — Packet Analysis Capability

The environment must support authorized packet capture and network analysis for:

- Troubleshooting
- Network education
- Security analysis
- Incident response
- Digital investigations

Packet analysis activities must remain within systems and networks the Stoneleaf Services lab is authorized to inspect.

---

## NR-25 — Digital Investigation Support

The network must support future digital investigation activities.

Potential requirements include:

- Investigation workstation connectivity
- Controlled evidence transfer
- Access to investigation resources
- Security-event correlation
- Logging
- Network analysis
- Controlled isolation of systems

Detailed investigation network requirements will be refined as investigation capabilities are introduced.

---

## NR-26 — Intelligence and Analysis Support

The network must support future intelligence and analysis activities.

Potential requirements include:

- Research connectivity
- Analytical workstations
- Controlled data repositories
- Internet resources
- Logging
- Access controls
- Future analytical platforms

Network access must remain consistent with organizational and security requirements.

---

## NR-27 — Sensitive Business Function Support

The network must be capable of supporting systems and resources containing sensitive organizational information.

This may include:

- Human Resources
- Finance
- Legal
- Compliance
- Investigations
- Intelligence
- Security operations

Sensitive information must be capable of receiving additional access controls where required.

---

## NR-28 — Future Server Expansion

The network must support future servers without requiring complete redesign.

Potential future infrastructure may include:

- File servers
- Logging servers
- Monitoring servers
- Security systems
- Application servers
- Databases
- Backup infrastructure
- Storage systems
- Investigation systems

Addressing and segmentation should reserve reasonable capacity for growth.

---

## NR-29 — Future Storage Infrastructure

The network must support future centralized storage or NAS infrastructure.

Future storage may support:

- Backups
- Documentation
- Lab data
- Security logs
- Investigation data
- Virtual-machine backups
- Other authorized organizational information

Storage architecture will be designed separately when introduced.

---

## NR-30 — Future Wireless Capability

The network architecture should be capable of supporting wireless networking if wireless infrastructure is introduced later.

Potential future requirements may include:

- Internal wireless access
- Administrative wireless access
- Guest access
- Device isolation
- VLAN integration
- Security monitoring

Wireless networking is not required for the initial virtual environment.

---

## NR-31 — Future VPN Capability

The network must support future secure remote or site-to-site VPN connectivity.

Potential use cases include:

- Administrative remote access
- Site-to-Site connectivity
- Cloud connectivity
- Future organizational expansion

VPN implementation is not required during the initial network deployment unless separately approved.

---

## NR-32 — Azure Connectivity

The network architecture must support future connectivity with Microsoft Azure.

Future connectivity may include:

- Azure Virtual Networks
- Cloud subnets
- Site-to-Site VPN
- Hybrid infrastructure
- Cloud-hosted servers
- Security services
- Monitoring services

The initial network design must avoid addressing decisions that unnecessarily complicate future Azure connectivity.

---

## NR-33 — Microsoft Entra Integration

The network must support future Microsoft Entra and hybrid identity capabilities.

Network architecture must permit appropriate communication with Microsoft cloud identity and management services.

Detailed Entra requirements will be defined during the Azure/Entra phase.

---

## NR-34 — Non-Overlapping Addressing

The network addressing architecture should avoid unnecessary address-space conflicts with future connected networks.

This is particularly important for:

- Azure
- VPN connections
- Additional Stoneleaf Services networks
- Future remote locations
- Future lab expansion

Final address spaces will be selected during the IP Addressing Plan.

---

## NR-35 — Scalability

The network must support expansion beyond the initial six permanent virtual machines.

Growth should be possible without requiring complete replacement of the initial architecture.

---

## NR-36 — Resource Efficiency

The network design must remain practical for a home-lab environment.

Architecture must balance:

- Realism
- Security
- Educational value
- Troubleshooting value
- Available computing resources
- Storage capacity
- Administrative complexity

Complexity must have a documented purpose.

---

## NR-37 — Availability

Core network services should be sufficiently reliable for the Stoneleaf Services lab environment.

The initial environment is not required to provide enterprise production-level high availability.

Future redundancy may be introduced when justified by educational, technical, or business requirements.

---

## NR-38 — Recoverability

Network configurations must be capable of being backed up and restored where supported.

This includes appropriate configuration backups for systems such as:

- pfSense
- VMware networking
- DNS
- DHCP-related configuration
- Future managed network infrastructure

Recovery procedures will be documented as systems are implemented.

---

## NR-39 — Change Management

Significant network changes must follow the Stoneleaf Services change-management process.

Examples include:

- Addressing changes
- Subnet changes
- VLAN creation
- DHCP changes
- DNS changes
- Routing changes
- NAT changes
- Firewall-rule changes
- VMware networking changes
- VPN changes
- Cloud-connectivity changes

Changes must include appropriate planning, validation, documentation, and rollback considerations.

---

## NR-40 — Documentation

The final network architecture must be documented sufficiently to allow another technically qualified individual to understand:

- Network structure
- Addressing
- Subnets
- Gateways
- Network segments
- VLANs
- DHCP
- DNS
- Routing
- NAT
- Firewall placement
- VMware networking
- Major traffic flows
- Security boundaries
- Future expansion

---

## NR-41 — Network Diagram

Stoneleaf Services must maintain a logical network diagram representing the approved network architecture.

The diagram should identify, where applicable:

- Network boundaries
- Firewall
- Network interfaces
- Subnets
- VLANs
- Servers
- Workstations
- Gateways
- Virtual networks
- Major traffic paths
- Future cloud connectivity

Planned components must not be represented as operational until they are implemented.

---

## NR-42 — Traffic Flow Documentation

Important network communications must be documented.

Traffic-flow records should identify:

**Source → Destination → Service/Protocol → Security Control → Expected Result**

This documentation will support:

- Firewall design
- Troubleshooting
- Security monitoring
- Incident response
- Architecture review

---

## NR-43 — Validation

The network design must define how successful implementation will be verified.

Validation must eventually include appropriate testing of:

- IP configuration
- DHCP
- DNS
- Gateway connectivity
- Routing
- NAT
- Firewall behavior
- Internal services
- Internet connectivity
- Domain services
- Linux connectivity
- Segmentation
- Security controls

---

## NR-44 — Security Validation

Network security controls must be tested to verify both:

- Authorized traffic succeeds.
- Unauthorized traffic is blocked where required.

Successful connectivity alone is not sufficient to validate a security design.

---

## NR-45 — Design Traceability

Major network design decisions should be traceable to one or more documented requirements.

The relationship should remain:

**Requirement → Design Decision → Configuration → Validation**

This provides evidence that technical architecture exists for a documented reason.

---

# Requirements Summary

The Stoneleaf Services network must provide:

1. Private internal networking
2. Defined network boundaries
3. Firewall protection
4. Routing
5. NAT
6. DHCP
7. Predictable infrastructure addressing
8. Internal DNS
9. Active Directory connectivity
10. Internet connectivity
11. Segmentation capability
12. VLAN capability
13. Controlled inter-segment communication
14. VMware virtual networking
15. Administrative connectivity
16. Windows and Linux connectivity
17. Security monitoring support
18. Logging support
19. Troubleshooting capability
20. Packet-analysis capability
21. Investigation support
22. Intelligence-analysis support
23. Sensitive-resource protection
24. Infrastructure expansion
25. Future storage support
26. Future wireless capability
27. Future VPN capability
28. Future Azure connectivity
29. Future Entra integration
30. Scalable addressing
31. Resource-efficient architecture
32. Recoverability
33. Change management
34. Architecture documentation
35. Network diagrams
36. Traffic-flow documentation
37. Functional validation
38. Security validation
39. Design traceability

---

# Current Design Decisions

At this stage, the following architectural directions have already been established:

| Requirement Area | Current Direction |
| --- | --- |
| Virtualization | VMware |
| Edge Firewall | pfSense (`SLS-FW01`) |
| DHCP | pfSense |
| Active Directory | Windows Server (`SLS-DC01`) |
| Internal DNS | Windows Server (`SLS-DC01`) |
| Linux | Ubuntu Server 24.04 LTS (`SLS-LNX01`) |
| Windows Endpoints | Windows 11 |
| Cloud Expansion | Microsoft Azure |
| Cloud Identity | Microsoft Entra ID |
| Segmentation | Required capability; final design pending |
| VLANs | Supported if justified; final design pending |
| IP Addressing | Final design pending |
| AD/DNS Namespace | Final design pending |
| VMware Networks | Final design pending |
| Firewall Rules | Final design pending |
| Hybrid Connectivity | Future phase |

---

# Deferred Design Decisions

The following decisions are intentionally deferred to subsequent Network Design documents:

- Final logical topology
- Private IP address space
- Subnet sizes
- Static-address ranges
- DHCP pools
- DHCP reservations
- VLAN count
- VLAN IDs
- VLAN names
- Network-segment purposes
- Default gateways
- VMware virtual networks
- pfSense interface assignments
- Routing configuration
- NAT configuration
- Firewall rules
- Traffic-flow permissions
- Future Azure network addressing
- Future VPN configuration

Deferring these decisions prevents configuration choices from being made before the architecture has been evaluated.

---

# Validation of Requirements

Before proceeding to implementation, each major network requirement should be represented by an architectural design decision or explicitly documented as deferred for future implementation.

Requirements that are not currently implemented may remain valid future requirements.

---

# Current Status

**Document:** Network Requirements  
**Phase:** `01-Network-Design`  
**Version:** 1.0  
**Status:** Complete for Initial Design  
**Deployment:** Not Started

These requirements establish the capabilities that the Stoneleaf Services network architecture must support.

---

# Next Document

The next Network Design document is:

`02-Logical-Network-Topology.md`

The Logical Network Topology will begin translating these requirements into an actual architecture by determining how the Stoneleaf Services network boundaries, pfSense firewall, VMware environment, servers, workstations, and future network segments should logically connect.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
