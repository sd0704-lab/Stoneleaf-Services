# Stoneleaf Services — IP Addressing Plan

**No Stone Left Unturned**

## Purpose

This document defines the IP addressing architecture for the Stoneleaf Services network.

The addressing plan establishes a structured private IPv4 address space that supports:

- Current VMware infrastructure
- pfSense
- Windows Server
- Active Directory
- Internal DNS
- Ubuntu Server
- Windows workstations
- Network segmentation
- Administrative access
- Security operations
- Digital investigations
- Lab and testing systems
- Future servers
- Future storage
- Future physical infrastructure
- Future Microsoft Azure connectivity

The addressing architecture is designed to remain simple enough for troubleshooting while providing substantial capacity for future expansion.

---

# Addressing Design Principles

The Stoneleaf Services addressing architecture follows these principles:

1. Use RFC 1918 private IPv4 addressing.
2. Maintain a dedicated Stoneleaf Services address space.
3. Separate on-premises and future Azure address spaces.
4. Use predictable subnet assignments.
5. Reserve addresses for future growth.
6. Provide consistent gateway conventions.
7. Separate static infrastructure addressing from dynamic client addressing.
8. Avoid unnecessary subnet complexity.
9. Make addresses understandable during troubleshooting.
10. Prevent address overlap with future Stoneleaf Services cloud networks.

---

# Primary Address Spaces

Stoneleaf Services will reserve the following private IPv4 address spaces:

| Environment | Address Space | Purpose |
| --- | --- | --- |
| Stoneleaf On-Premises | `10.10.0.0/16` | VMware, physical infrastructure, endpoints, servers, security zones, and future local expansion |
| Stoneleaf Azure | `10.20.0.0/16` | Future Microsoft Azure virtual networks and cloud resources |

These address spaces are intentionally separate.

The separation allows future VPN or hybrid routing between Stoneleaf Services on-premises and Azure without requiring overlapping address translation.

---

# On-Premises Address Space

The primary Stoneleaf Services on-premises address space is:

`10.10.0.0/16`

Subnet mask:

`255.255.0.0`

Address range:

`10.10.0.0` through `10.10.255.255`

This `/16` is the overall addressing block reserved for Stoneleaf Services local infrastructure.

Individual systems will not normally operate directly on a `/16` subnet.

The `/16` will instead be divided into smaller functional networks.

---

# Subnet Allocation Strategy

Stoneleaf Services will generally allocate `/24` networks from the `10.10.0.0/16` address space.

A `/24` provides:

- 256 total addresses
- 254 usable host addresses
- Simple subnet identification
- Easy documentation
- Straightforward troubleshooting
- Sufficient capacity for the Stoneleaf Services lab

Subnet mask:

`255.255.255.0`

Example:

`10.10.10.0/24`

Usable hosts:

`10.10.10.1` through `10.10.10.254`

Broadcast:

`10.10.10.255`

---

# Functional Network Allocation

The following network ranges are reserved for Stoneleaf Services functional zones.

| Network | Address Space | Function | Status |
| --- | --- | --- | --- |
| Infrastructure | `10.10.10.0/24` | Core servers and infrastructure | Planned |
| User Endpoints | `10.10.20.0/24` | Standard organizational endpoints | Planned |
| Management | `10.10.30.0/24` | Administrative and infrastructure management | Reserved |
| Security Operations | `10.10.40.0/24` | Security monitoring and security systems | Reserved |
| Investigations | `10.10.50.0/24` | Digital investigation systems and resources | Reserved |
| Lab / Testing | `10.10.60.0/24` | Testing, training, temporary systems, and isolated labs | Reserved |
| Storage / Backup | `10.10.70.0/24` | Future NAS, backup, and storage infrastructure | Reserved |
| Network Infrastructure | `10.10.80.0/24` | Future physical network infrastructure | Reserved |

The remaining `10.10.0.0/16` address space remains available for future requirements.

---

# Reserved Address Space

The following ranges remain intentionally unassigned:

`10.10.0.0/24`

`10.10.90.0/24` through `10.10.255.0/24`

These networks provide substantial room for future:

- Additional security zones
- Additional server networks
- Wireless networks
- Guest networks
- Additional labs
- Physical infrastructure
- Remote sites
- Specialized investigation environments
- Development environments
- Additional storage networks
- Future Stoneleaf Services capabilities

Networks will not be assigned until a documented requirement exists.

---

# Gateway Standard

Where practical, Stoneleaf Services will use the first usable address in each subnet as the default gateway.

Standard:

`10.10.X.1`

Examples:

| Network | Gateway |
| --- | --- |
| Infrastructure | `10.10.10.1` |
| User Endpoints | `10.10.20.1` |
| Management | `10.10.30.1` |
| Security Operations | `10.10.40.1` |
| Investigations | `10.10.50.1` |
| Lab / Testing | `10.10.60.1` |
| Storage / Backup | `10.10.70.1` |
| Network Infrastructure | `10.10.80.1` |

These gateway addresses will normally correspond to pfSense interfaces or logical interfaces associated with the network.

---

# Address Allocation Standard

Within each `/24`, Stoneleaf Services will use a consistent address-allocation model.

| Range | Purpose |
| --- | --- |
| `.1` | Default gateway |
| `.2 – .9` | Network infrastructure / reserved |
| `.10 – .49` | Servers and infrastructure |
| `.50 – .99` | Reserved static systems / appliances |
| `.100 – .199` | DHCP clients |
| `.200 – .239` | Specialized or temporary static assignments |
| `.240 – .254` | Reserved for future use |

This convention provides predictable addressing across Stoneleaf Services networks.

Not every subnet must use every range.

---

# Infrastructure Network

Network:

`10.10.10.0/24`

Purpose:

Core Stoneleaf Services server infrastructure.

Default gateway:

`10.10.10.1`

Initial planned systems include:

| Address | System | Function |
| --- | --- | --- |
| `10.10.10.1` | `SLS-FW01` | Infrastructure gateway |
| `10.10.10.10` | `SLS-DC01` | Active Directory Domain Services / DNS |
| `10.10.10.20` | `SLS-LNX01` | Ubuntu Server |

Future systems may include:

- File servers
- Application servers
- Logging infrastructure
- Monitoring systems
- Internal services

Additional infrastructure addresses will be assigned as requirements develop.

---

# User Endpoint Network

Network:

`10.10.20.0/24`

Purpose:

Standard Stoneleaf Services organizational endpoints.

Default gateway:

`10.10.20.1`

Initial workstations include:

- `SLS-WS01`
- `SLS-WS02`
- `SLS-WS03`

These systems are expected to receive addresses dynamically unless a future technical requirement justifies static addressing or DHCP reservations.

Proposed DHCP range:

`10.10.20.100 – 10.10.20.199`

Final DHCP configuration will be documented in:

`06-DHCP-Design.md`

---

# Management Network

Network:

`10.10.30.0/24`

Purpose:

Restricted administrative and infrastructure-management traffic.

Default gateway:

`10.10.30.1`

Potential future systems or interfaces include:

- Administrative workstation
- VMware management
- pfSense management
- Server-management interfaces
- Managed switch interfaces
- Wireless infrastructure
- Storage-management interfaces

This network is reserved until the Management Zone implementation is finalized.

---

# Security Operations Network

Network:

`10.10.40.0/24`

Purpose:

Security monitoring and security operations.

Default gateway:

`10.10.40.1`

Potential future systems include:

- SIEM
- Log collectors
- Security monitoring
- Vulnerability-management systems
- Detection systems
- Security-analysis systems

This network is reserved until security infrastructure is introduced.

---

# Investigation Network

Network:

`10.10.50.0/24`

Purpose:

Digital investigation systems and investigation resources.

Default gateway:

`10.10.50.1`

Potential future systems include:

- Forensic analysis workstation
- Evidence-processing systems
- Investigation servers
- Evidence storage
- Incident-analysis systems

The initial `SLS-WS01` workstation may remain on the User Endpoint network until dedicated investigation segmentation is justified and implemented.

---

# Lab / Testing Network

Network:

`10.10.60.0/24`

Purpose:

Controlled testing and experimentation.

Default gateway:

`10.10.60.1`

Potential systems include:

- Temporary virtual machines
- Test servers
- Security-testing systems
- Vulnerable systems
- Troubleshooting labs
- Training systems
- Temporary Kali Linux systems
- Experimental configurations

This network should eventually support stronger isolation from normal Stoneleaf Services infrastructure.

---

# Storage / Backup Network

Network:

`10.10.70.0/24`

Purpose:

Future storage and backup infrastructure.

Default gateway:

`10.10.70.1`

Potential future systems include:

- NAS
- Backup server
- VM backup repository
- Log storage
- Documentation storage
- Investigation storage

This network is reserved until storage architecture is designed.

---

# Network Infrastructure Network

Network:

`10.10.80.0/24`

Purpose:

Future physical network infrastructure.

Default gateway:

`10.10.80.1`

Potential future devices include:

- Managed switches
- Wireless access points
- Network controllers
- Infrastructure-management devices
- Additional network appliances

This network is reserved until physical network infrastructure is introduced.

---

# Initial Static Address Assignments

The following initial addresses are established:

| Hostname | Address | Network | Assignment |
| --- | --- | --- | --- |
| `SLS-FW01` | `10.10.10.1` | Infrastructure | Gateway |
| `SLS-DC01` | `10.10.10.10` | Infrastructure | Static |
| `SLS-LNX01` | `10.10.10.20` | Infrastructure | Static |

Workstation addresses will initially be provided through DHCP.

---

# DNS Addressing

`SLS-DC01` will provide internal DNS.

Primary internal DNS server:

`10.10.10.10`

Domain-joined systems will use:

`10.10.10.10`

as their primary DNS server.

Clients should not use public DNS servers directly as alternate DNS servers for the Active Directory environment.

External DNS queries will be resolved through the internal DNS architecture.

---

# DHCP Addressing

pfSense will provide DHCP for applicable Stoneleaf Services networks.

DHCP ranges will generally use:

`.100 – .199`

where appropriate.

Example:

User Endpoint Network:

`10.10.20.100 – 10.10.20.199`

DHCP scopes will provide the appropriate:

- IP address
- Subnet mask
- Default gateway
- Internal DNS server
- Required domain options

Final DHCP scope definitions will be documented separately.

---

# Static Addressing

Static addressing should be used for systems requiring predictable network locations.

Examples include:

- Firewalls
- Domain controllers
- DNS servers
- Servers
- Network infrastructure
- Storage infrastructure
- Logging systems
- Monitoring systems

Static assignments must be documented.

---

# DHCP Reservations

DHCP reservations may be used when a system benefits from predictable addressing while remaining centrally managed through DHCP.

Potential uses include:

- Specific workstations
- Appliances
- Printers
- Network devices
- Test systems

Reservations will be documented in the DHCP Design.

---

# IPv6

IPv6 is not part of the initial Stoneleaf Services network design.

The initial lab will focus on IPv4 to support:

- Network fundamentals
- Routing
- Subnetting
- DHCP
- DNS
- Firewalling
- NAT
- Troubleshooting
- Security monitoring

IPv6 may be introduced later as a dedicated expansion or training objective.

IPv6 should not be considered permanently excluded from Stoneleaf Services architecture.

---

# Azure Address Space

Stoneleaf Services reserves:

`10.20.0.0/16`

for future Microsoft Azure infrastructure.

This space is separate from the on-premises:

`10.10.0.0/16`

network.

Potential future Azure allocation may include:

| Example Network | Potential Function |
| --- | --- |
| `10.20.10.0/24` | Azure Infrastructure |
| `10.20.20.0/24` | Azure Application Systems |
| `10.20.30.0/24` | Azure Management |
| `10.20.40.0/24` | Azure Security |
| Additional Networks | Future Requirements |

These Azure subnet assignments are examples only.

Final Azure subnet architecture will be established during the Azure/Entra phase.

---

# Hybrid Routing Consideration

The non-overlapping address spaces allow future routing between:

**Stoneleaf On-Premises**

`10.10.0.0/16`

and:

**Stoneleaf Azure**

`10.20.0.0/16`

Conceptually:

    Stoneleaf On-Premises
        10.10.0.0/16
              |
           SLS-FW01
              |
       Site-to-Site VPN
              |
         Microsoft Azure
        10.20.0.0/16

This avoids requiring address translation between the two Stoneleaf environments solely because of overlapping internal address space.

---

# Existing Home Network

The existing home network remains outside the Stoneleaf Services internal addressing architecture.

Stoneleaf Services systems should not use the home network's internal addressing as their primary internal lab network.

The relationship remains:

    Internet
       |
    Home Network
       |
    VMware Host
       |
    SLS-FW01
       |
    10.10.0.0/16
    Stoneleaf Services

The exact upstream address assigned to the pfSense WAN interface will depend on the existing home network and VMware configuration.

It is therefore not permanently defined in this document.

---

# Address Documentation

Every permanently assigned static address should eventually be documented with:

- Hostname
- IP address
- Subnet
- Gateway
- DNS configuration
- Assignment type
- System function
- Associated network
- Status

This provides a central reference for troubleshooting and infrastructure management.

---

# Address Conflict Prevention

Before assigning a static address:

1. Verify the address belongs to the correct subnet.
2. Verify the address is not inside an active DHCP pool unless reserved appropriately.
3. Verify the address is not already assigned.
4. Verify the assignment follows the addressing standard.
5. Record the assignment in the appropriate documentation.

---

# Troubleshooting Benefits

The addressing convention is designed to make addresses meaningful during troubleshooting.

Examples:

`10.10.10.x`

indicates Infrastructure.

`10.10.20.x`

indicates User Endpoints.

`10.10.30.x`

indicates Management.

`10.10.40.x`

indicates Security Operations.

`10.10.50.x`

indicates Investigations.

`10.10.60.x`

indicates Lab / Testing.

`10.10.70.x`

indicates Storage / Backup.

`10.10.80.x`

indicates Network Infrastructure.

This allows an administrator reviewing an address to quickly identify its general network function.

---

# Scalability

The addressing architecture provides substantial expansion capacity.

Only a small portion of:

`10.10.0.0/16`

is initially allocated.

Additional `/24` networks can be assigned as new requirements emerge without renumbering existing networks.

This supports future:

- Servers
- Security infrastructure
- Storage
- Wireless
- Guest networking
- Additional labs
- Additional virtualization hosts
- Physical infrastructure
- Specialized investigation systems
- Additional Stoneleaf Services capabilities

---

# Security Considerations

IP addressing does not provide security by itself.

Separate subnets must be combined with appropriate controls such as:

- Firewall rules
- Routing policy
- Identity controls
- Authentication
- Authorization
- Endpoint security
- Logging
- Monitoring

Placement in a different subnet does not automatically prevent communication.

Security policy will determine which networks may communicate.

---

# Addressing Summary

| Function | Network | Gateway | Status |
| --- | --- | --- | --- |
| Infrastructure | `10.10.10.0/24` | `10.10.10.1` | Planned |
| User Endpoints | `10.10.20.0/24` | `10.10.20.1` | Planned |
| Management | `10.10.30.0/24` | `10.10.30.1` | Reserved |
| Security Operations | `10.10.40.0/24` | `10.10.40.1` | Reserved |
| Investigations | `10.10.50.0/24` | `10.10.50.1` | Reserved |
| Lab / Testing | `10.10.60.0/24` | `10.10.60.1` | Reserved |
| Storage / Backup | `10.10.70.0/24` | `10.10.70.1` | Reserved |
| Network Infrastructure | `10.10.80.0/24` | `10.10.80.1` | Reserved |
| Future On-Premises | Remaining `10.10.0.0/16` | TBD | Reserved |
| Future Azure | `10.20.0.0/16` | TBD | Reserved |

---

# Initial Address Summary

| System | Address |
| --- | --- |
| `SLS-FW01` Infrastructure Gateway | `10.10.10.1` |
| `SLS-DC01` | `10.10.10.10` |
| `SLS-LNX01` | `10.10.10.20` |
| Internal DNS | `10.10.10.10` |
| User DHCP Pool | `10.10.20.100 – 10.10.20.199` |

Additional addresses will be assigned only as systems are introduced.

---

# Design Decisions Established

This document establishes:

1. Stoneleaf Services on-premises address space: `10.10.0.0/16`.
2. Future Azure address space: `10.20.0.0/16`.
3. Functional networks will generally use `/24` subnets.
4. Gateways will generally use `.1`.
5. Servers and infrastructure will generally use `.10 – .49`.
6. DHCP clients will generally use `.100 – .199`.
7. `SLS-DC01` will use `10.10.10.10`.
8. `SLS-LNX01` will use `10.10.10.20`.
9. `SLS-DC01` will provide internal DNS at `10.10.10.10`.
10. Infrastructure will use `10.10.10.0/24`.
11. User Endpoints will use `10.10.20.0/24`.
12. Management will reserve `10.10.30.0/24`.
13. Security Operations will reserve `10.10.40.0/24`.
14. Investigations will reserve `10.10.50.0/24`.
15. Lab / Testing will reserve `10.10.60.0/24`.
16. Storage / Backup will reserve `10.10.70.0/24`.
17. Network Infrastructure will reserve `10.10.80.0/24`.
18. Remaining on-premises address space will remain available for future requirements.
19. IPv4 will be used for the initial environment.
20. IPv6 may be introduced later as a separate expansion.

---

# Decisions Still Pending

The following remain to be designed:

- Final segmentation implementation
- VLAN assignments
- VLAN IDs
- Exact DHCP scopes for additional networks
- Additional static addresses
- pfSense interface assignments
- VMware virtual network mappings
- Inter-network routing policies
- Firewall rules
- Management Zone implementation
- Security Operations implementation
- Investigation Zone implementation
- Storage implementation
- Azure subnet architecture
- VPN addressing
- IPv6 implementation

---

# Validation Criteria

The addressing plan is considered valid if:

- Every network uses private IPv4 addressing.
- On-premises and Azure address spaces do not overlap.
- Each functional subnet has sufficient capacity.
- Gateway conventions are consistent.
- Static and dynamic addressing can coexist without conflict.
- Infrastructure addresses are predictable.
- DHCP space is clearly separated.
- Future networks can be added without renumbering existing networks.
- Addresses are understandable during troubleshooting.
- The architecture supports future hybrid connectivity.

---

# Current Status

**Document:** IP Addressing Plan  
**Phase:** `01-Network-Design`  
**Version:** 1.0  
**Status:** Complete for Initial Design  
**Deployment:** Not Started

The Stoneleaf Services private IPv4 addressing architecture is now established.

---

# Next Document

The next Network Design document is:

`04-Subnet-and-Segmentation-Plan.md`

The Subnet and Segmentation Plan will determine which of the reserved networks should be implemented initially and which should remain reserved for future use.

It will also define the security and operational justification for separating systems into different network segments.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
