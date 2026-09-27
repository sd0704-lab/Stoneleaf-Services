# Stoneleaf Services — Logical Network Topology

**No Stone Left Unturned**

## Purpose

This document defines the logical network topology for the Stoneleaf Services technical environment.

The logical topology translates the capabilities established in `01-Network-Requirements.md` into an organized network architecture.

This document determines:

- The major network boundaries.
- The position and role of the pfSense firewall.
- How VMware participates in the network architecture.
- How Stoneleaf Services servers and workstations logically connect.
- Which major security zones are required.
- How traffic moves between internal systems and external networks.
- How future network expansion can be incorporated.

This document defines logical relationships rather than final addressing or configuration.

Specific IP addresses, subnet sizes, VLAN IDs, DHCP scopes, routing entries, NAT configuration, and firewall rules are defined in later Network Design documents.

---

# Design Goals

The Stoneleaf Services logical network topology must:

- Provide a defined boundary between Stoneleaf Services and external networks.
- Route Stoneleaf Services traffic through `SLS-FW01`.
- Support controlled communication between internal network segments.
- Support Active Directory and internal DNS.
- Support Windows and Linux systems.
- Support administrative access.
- Support cybersecurity operations.
- Support digital investigation activities.
- Support intelligence and analysis activities.
- Support security logging and monitoring.
- Support future infrastructure growth.
- Support future Azure connectivity.
- Remain practical for a VMware-based home lab.
- Avoid unnecessary complexity.
- Support systematic troubleshooting.

---

# High-Level Architecture

The Stoneleaf Services environment will use a firewall-centered architecture.

The primary logical path is:

**External Network / Internet → VMware External Network → SLS-FW01 → Stoneleaf Internal Networks → Servers and Endpoints**

`SLS-FW01` will function as the primary logical boundary between Stoneleaf Services internal networks and external connectivity.

Internal systems will not bypass `SLS-FW01` for normal external network access.

---

# Primary Network Components

## External Network

The external network represents connectivity outside the Stoneleaf Services controlled environment.

This may include:

- The existing home network
- Internet connectivity
- External DNS resources
- Software repositories
- Vendor services
- Microsoft cloud services
- Future remote resources

The existing home network is not considered part of the Stoneleaf Services internal network.

---

## VMware Host

The VMware host provides the virtualization platform for the Stoneleaf Services environment.

The VMware host will provide virtual networking required to connect:

- `SLS-FW01`
- `SLS-DC01`
- `SLS-LNX01`
- `SLS-WS01`
- `SLS-WS02`
- `SLS-WS03`
- Future virtual systems

VMware virtual networking will provide separation between external connectivity and Stoneleaf Services internal networks.

Detailed VMware network configuration will be documented in:

`11-VMware-Network-Design.md`

---

# SLS-FW01

`SLS-FW01` is the planned pfSense firewall/router.

It will form the primary network boundary for the Stoneleaf Services environment.

Its responsibilities will include:

- Firewall enforcement
- Routing
- DHCP
- NAT
- Network segmentation
- Traffic logging
- Inter-network communication control
- Future VPN connectivity
- Future hybrid connectivity

`SLS-FW01` must have at least two logical network interfaces:

1. External / WAN
2. Internal / LAN

Additional logical interfaces may be introduced as segmentation is implemented.

The final interface architecture will be determined after the segmentation design is completed.

---

# WAN / External Boundary

The WAN side of `SLS-FW01` connects Stoneleaf Services to the external network through VMware.

Conceptually:

**Internet → Existing Home Network → VMware External Network → SLS-FW01 WAN**

The WAN interface is not considered a trusted Stoneleaf Services network.

Inbound access from the external network must be denied unless explicitly required and authorized.

---

# Internal Network Boundary

The internal side of `SLS-FW01` connects to the Stoneleaf Services controlled network environment.

All permanent Stoneleaf Services virtual systems will reside behind this boundary.

Internal traffic will be divided into logical security zones as the environment develops.

---

# Logical Security Zones

Stoneleaf Services will use **functional security zones rather than creating one network for every organizational department**.

This prevents the network design from unnecessarily mirroring the organizational chart.

The initial logical architecture will support the following zone concepts.

---

# Infrastructure Zone

The Infrastructure Zone will contain systems providing core organizational services.

Potential systems include:

- `SLS-DC01`
- Future file servers
- Future logging servers
- Future monitoring servers
- Future application servers
- Future backup infrastructure

The Infrastructure Zone represents systems that provide services to other Stoneleaf Services systems.

Access to infrastructure resources should be limited to required services.

---

# User Endpoint Zone

The User Endpoint Zone will support normal organizational workstations.

The initial systems include:

- `SLS-WS01`
- `SLS-WS02`
- `SLS-WS03`

Although these systems perform different organizational functions, they do not automatically require separate network segments.

Access differences may initially be enforced through:

- Active Directory
- Security groups
- Resource permissions
- Group Policy
- Application controls
- Host security controls
- Firewall policy where appropriate

Additional segmentation may be introduced if future requirements justify it.

---

# Management Zone

The architecture will support a dedicated Management Zone.

The Management Zone is intended for administrative access to infrastructure rather than ordinary user activity.

Potential management targets include:

- pfSense
- Windows Server
- Linux servers
- VMware
- Future network infrastructure
- Future monitoring systems
- Future storage infrastructure

The Management Zone may eventually contain:

- Administrative workstations
- Management interfaces
- Administrative services
- Infrastructure-management tools

Whether the Management Zone is implemented immediately or reserved for future deployment will be determined during segmentation design.

---

# Security Operations Zone

The architecture will support a Security Operations Zone if required.

Potential systems may include:

- Security monitoring platforms
- SIEM infrastructure
- Log collectors
- Security-analysis systems
- Vulnerability-management systems
- Detection systems

Security infrastructure often requires visibility into multiple systems while remaining protected from ordinary user access.

The exact implementation will be determined as Stoneleaf Services security capabilities develop.

---

# Investigation Zone

The architecture will support a controlled Investigation Zone.

Potential uses include:

- Digital forensic analysis
- Evidence processing
- Investigation systems
- Controlled evidence storage
- Incident analysis
- Malware analysis environments where separately authorized and isolated

Investigation systems may require greater isolation than ordinary organizational endpoints.

The exact implementation will be determined during later investigation and security design phases.

---

# Lab / Testing Zone

Stoneleaf Services will support an isolated Lab / Testing Zone.

This zone may eventually contain:

- Temporary virtual machines
- Security testing systems
- Experimental servers
- Training environments
- Intentionally misconfigured systems
- Vulnerable systems
- Troubleshooting exercises
- Temporary Kali Linux systems
- Other authorized test systems

The Lab / Testing Zone must be capable of being isolated from normal Stoneleaf Services infrastructure.

This allows experiments to occur without unnecessarily exposing production-like lab services.

---

# Future Storage Zone

The architecture must support future centralized storage.

Potential systems may include:

- NAS
- Backup server
- VM backup storage
- Documentation storage
- Security-log storage
- Investigation storage

Storage may require a dedicated security boundary depending on future requirements.

A separate storage network will not be created until justified.

---

# Future Cloud Zone

Microsoft Azure will eventually extend the Stoneleaf Services architecture into a hybrid environment.

Future cloud infrastructure may include:

- Azure Virtual Network
- Cloud subnets
- Virtual machines
- Security services
- Logging services
- Microsoft Entra integration
- Site-to-Site VPN connectivity

The on-premises addressing architecture must therefore avoid unnecessary conflicts with future Azure networks.

Detailed hybrid architecture will be developed later.

---

# Initial System Placement

The initial logical placement of the six permanent systems is:

| System | Logical Function | Initial Zone |
| --- | --- | --- |
| `SLS-FW01` | Firewall / Router | Network Boundary |
| `SLS-DC01` | Active Directory / DNS | Infrastructure |
| `SLS-LNX01` | Linux Server | Infrastructure |
| `SLS-WS01` | Investigations Workstation | User Endpoint |
| `SLS-WS02` | Intelligence / Analysis Workstation | User Endpoint |
| `SLS-WS03` | Management / Administrative Workstation | User Endpoint initially |

`SLS-WS03` may later be moved to or supplemented by a dedicated Management Zone if the segmentation design determines that administrative isolation is appropriate.

---

# Logical Topology

The initial architecture can be represented conceptually as:

    Internet
       |
       |
    Existing Home Network
       |
       |
    VMware External Network
       |
       |
    SLS-FW01
    pfSense
       |
       |
    Stoneleaf Internal Network
       |
       +----------------------+
       |                      |
       |                      |
    Infrastructure         User Endpoints
       |                      |
       |                      |
    SLS-DC01              SLS-WS01
    SLS-LNX01             SLS-WS02
                          SLS-WS03

The architecture will later expand to support additional security zones:

    Internet
       |
    Existing Home Network
       |
    VMware External Network
       |
    SLS-FW01
       |
       +--------------------------------------------------+
       |             |              |          |          |
       |             |              |          |          |
 Infrastructure   Endpoints     Management   Security   Lab/Test
                                             Operations
       |
       |
 Future Internal Services

Additional zones may be introduced only when justified by documented requirements.

---

# Traffic Control Model

`SLS-FW01` will serve as the primary control point for traffic crossing network boundaries.

The general model will be:

**Source Zone → SLS-FW01 → Policy Decision → Destination Zone**

Traffic should not automatically be allowed simply because both systems are part of Stoneleaf Services.

Communication should exist because a documented service or operational requirement requires it.

---

# Default Security Philosophy

The architecture will follow the principle:

**Allow required communication. Restrict unnecessary communication.**

This principle will later be translated into specific firewall policies.

Examples may include:

- User endpoints require DNS access to internal DNS.
- Domain clients require access to Active Directory services.
- Systems may require controlled internet access.
- Administrators require management access to authorized infrastructure.
- Ordinary users should not require unrestricted access to management interfaces.
- Lab systems should not automatically communicate with sensitive infrastructure.
- Investigation systems may require controlled access to evidence resources.
- Monitoring systems may require access to logs from multiple network zones.

Specific ports, protocols, sources, destinations, and firewall rules will be documented later.

---

# Active Directory Traffic

`SLS-DC01` will provide Active Directory Domain Services and internal DNS.

Domain-joined Windows systems must be able to communicate with `SLS-DC01` for required domain services.

The logical relationship is:

**Domain Client → Internal Network → SLS-DC01**

Required Active Directory traffic will be identified in the Traffic Flow Matrix.

---

# DNS Traffic

Stoneleaf Services domain clients will use `SLS-DC01` for internal DNS.

Conceptually:

**Client → SLS-DC01 → Internal DNS Resolution**

For external name resolution:

**Client → SLS-DC01 → DNS Forwarding / External Resolution**

Domain clients should not bypass the internal DNS architecture by directly using public DNS unless a specific design requirement exists.

---

# DHCP Traffic

pfSense is planned to provide DHCP.

Conceptually:

**Client → Local Network → SLS-FW01 DHCP Service**

DHCP will eventually provide:

- IP address
- Subnet information
- Default gateway
- Internal DNS server
- Other required options

Specific DHCP scopes will be determined after the addressing and segmentation plans are complete.

---

# Internet Traffic

Normal internet traffic will follow:

**Internal System → SLS-FW01 → NAT → External Network → Internet**

Return traffic will follow the established state back through `SLS-FW01`.

Internal systems should not require direct exposure to the internet for ordinary outbound connectivity.

---

# Administrative Traffic

Administrative access must be distinguishable from ordinary user activity.

The future logical model is:

**Authorized Administrator → Management Path → Authorized Infrastructure**

Potential management targets include:

- `SLS-FW01`
- `SLS-DC01`
- `SLS-LNX01`
- VMware
- Future servers
- Future network infrastructure
- Future security infrastructure

The exact Management Zone implementation will be determined during segmentation design.

---

# Lab and Testing Traffic

The Lab / Testing Zone must be capable of being restricted from normal infrastructure.

The desired logical relationship is:

**Lab/Test System → Firewall Policy → Explicitly Authorized Resources**

rather than:

**Lab/Test System → Unrestricted Internal Network**

This provides a safer environment for:

- Security testing
- Troubleshooting
- Experimental configurations
- Vulnerable systems
- Temporary security tools

---

# Logging and Monitoring Traffic

Future monitoring infrastructure may need to receive information from multiple network zones.

Conceptually:

**Managed System → Logging / Monitoring System**

Security-monitoring infrastructure should not require unrestricted reciprocal access to every monitored system.

Detailed logging architecture will be developed later.

---

# Network Segmentation Philosophy

Stoneleaf Services will not create network segments solely because the technology supports them.

Each segment must provide a documented benefit such as:

- Security isolation
- Administrative separation
- Traffic control
- Testing isolation
- Monitoring
- Risk reduction
- Troubleshooting
- Service separation

This prevents unnecessary complexity while preserving the ability to build a realistic segmented environment.

---

# Department vs. Network Zone

The Stoneleaf Services organizational structure contains:

- Executive Leadership
- Information Technology
- Cybersecurity
- Digital Investigations
- Intelligence & Analysis
- Business Operations
- Project & Client Services
- Legal & Compliance

These departments will **not automatically receive individual VLANs or subnets**.

Organizational access will primarily be controlled through:

- Identity
- Security groups
- Resource permissions
- Application authorization
- Group Policy
- Endpoint controls

Network segmentation will be used when a network-level security boundary provides a meaningful benefit.

---

# VMware Boundary

The Stoneleaf Services network will initially exist primarily inside the VMware environment.

The logical boundary must prevent internal lab systems from bypassing pfSense when communicating externally.

The design must support:

**VMware Host**

→ External VMware Network

→ `SLS-FW01` WAN

→ `SLS-FW01` LAN / Internal Interfaces

→ Stoneleaf Services Internal Networks

This architecture allows pfSense to function as the network gateway rather than allowing each VM to connect directly to the home network.

---

# Physical Network Relationship

The existing physical home network provides upstream connectivity.

The Stoneleaf Services virtual network remains logically separate from the home network.

The relationship is:

**Internet**

↓

**Home Router / Existing Network**

↓

**VMware Host**

↓

**SLS-FW01**

↓

**Stoneleaf Services Networks**

The home router remains upstream of the Stoneleaf Services lab firewall.

Stoneleaf Services internal systems remain behind `SLS-FW01`.

---

# Future Physical Infrastructure

The architecture may later expand beyond a single VMware host.

Potential future infrastructure may include:

- Managed switch
- Wireless access point
- Additional virtualization hosts
- Physical servers
- NAS / storage server
- Dedicated security systems
- Additional workstations

The logical architecture should allow these systems to be integrated without requiring complete redesign.

---

# Future Hybrid Topology

Future Azure integration may extend the architecture to:

    Stoneleaf Services
    Internal Networks
          |
       SLS-FW01
          |
     Secure VPN
          |
      Microsoft Azure
          |
       Azure VNet
          |
    Cloud Resources

Specific Azure networks and VPN architecture will be developed during the hybrid-cloud design phase.

---

# High-Level Trust Model

The logical topology recognizes different levels of trust.

Potential trust relationships include:

| Zone | General Trust Consideration |
| --- | --- |
| External / WAN | Untrusted |
| User Endpoints | Standard Internal |
| Infrastructure | Protected |
| Management | Highly Restricted |
| Security Operations | Restricted |
| Investigations | Restricted |
| Lab / Testing | Isolated / Low Trust |
| Future Storage | Protected |
| Future Cloud | Controlled / Hybrid |

These classifications are architectural guidance.

Specific security controls will be determined later.

---

# Design Decisions Established

This document establishes the following decisions:

1. `SLS-FW01` will form the primary Stoneleaf Services network boundary.
2. Internal systems will reside behind `SLS-FW01`.
3. Normal external traffic will pass through `SLS-FW01`.
4. pfSense will provide routing, firewalling, NAT, and DHCP.
5. `SLS-DC01` will provide internal Active Directory DNS.
6. VMware will provide the initial virtual network infrastructure.
7. The home network will remain outside the Stoneleaf Services internal environment.
8. Network segmentation will be based on function and security requirements rather than organizational departments.
9. Infrastructure and user endpoints represent distinct logical functions.
10. The architecture will support a dedicated Management Zone.
11. The architecture will support a Security Operations Zone.
12. The architecture will support an isolated Lab / Testing Zone.
13. The architecture will support controlled investigation capabilities.
14. Future storage infrastructure can receive additional isolation if justified.
15. The addressing architecture must accommodate future Azure connectivity.
16. Network complexity must have a documented purpose.

---

# Decisions Not Yet Established

The following remain intentionally undecided:

- Final private IP address space
- Subnet sizes
- Number of deployed subnets
- VLAN count
- VLAN IDs
- VLAN names
- Default gateway addresses
- Static IP assignments
- DHCP pools
- DHCP reservations
- Exact VMware virtual networks
- pfSense interface count
- Exact firewall rules
- Exact inter-zone permissions
- NAT configuration
- Management Zone implementation timing
- Security Operations Zone implementation timing
- Investigation Zone implementation timing
- Storage network implementation
- Azure address space
- VPN configuration

These decisions will be made in subsequent Network Design documents.

---

# Validation Criteria

The logical topology is considered valid if it:

- Places internal systems behind the Stoneleaf Services firewall.
- Provides a clear external/internal boundary.
- Supports Active Directory.
- Supports internal DNS.
- Supports DHCP.
- Supports internet access.
- Supports Windows and Linux systems.
- Supports future segmentation.
- Supports controlled inter-network communication.
- Supports administrative access.
- Supports security monitoring.
- Supports investigation activities.
- Supports isolated testing.
- Supports future infrastructure.
- Supports future Azure connectivity.
- Remains practical for the available home-lab environment.
- Can be explained and troubleshot systematically.

---

# Current Status

**Document:** Logical Network Topology  
**Phase:** `01-Network-Design`  
**Version:** 1.0  
**Status:** Complete for Initial Design  
**Deployment:** Not Started

This document establishes the high-level logical architecture of the Stoneleaf Services network.

Specific network addressing and segmentation decisions remain intentionally deferred.

---

# Next Document

The next Network Design document is:

`03-IP-Addressing-Plan.md`

The IP Addressing Plan will select the Stoneleaf Services private address space and establish how addressing will be allocated for:

- Network infrastructure
- Servers
- Endpoints
- Static systems
- DHCP
- Future network segments
- Future infrastructure
- Future Azure connectivity

The addressing plan will be designed with sufficient capacity for growth while avoiding unnecessary complexity.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
