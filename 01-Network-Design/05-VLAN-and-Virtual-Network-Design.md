# Stoneleaf Services — VLAN and Virtual Network Design

**No Stone Left Unturned**

## Purpose

This document defines the VLAN and VMware virtual networking architecture for the Stoneleaf Services environment.

The Network Requirements, Logical Network Topology, IP Addressing Plan, and Subnet and Segmentation Plan establish the network capabilities, addressing standards, and security boundaries required by Stoneleaf Services.

This document translates those requirements into a virtual network architecture that can be implemented within VMware.

The initial environment will use separate VMware virtual networks to provide network segmentation without requiring physical managed switches or IEEE 802.1Q VLAN tagging.

The architecture must support future expansion into VLAN-based physical networking without requiring significant changes to the existing IP addressing scheme.

The finalized architecture is approved as the initial design baseline. All configurations described in this document are **planned** and have not yet been implemented or validated. Design approval does not establish implementation or validation completion.

---

# Design Objectives

The VLAN and Virtual Network Design must:

1. Provide separate virtual networks for the initial Stoneleaf Services security zones.
2. Support controlled routing between networks through pfSense.
3. Prevent unnecessary direct communication between security zones.
4. Support centralized DHCP and internal DNS services.
5. Support Active Directory authentication across approved network boundaries.
6. Provide a restricted network for infrastructure administration.
7. Provide an isolated environment for testing and experimentation.
8. Support internet connectivity through the Stoneleaf Services firewall.
9. Avoid unnecessary complexity during the initial deployment.
10. Support future physical VLAN implementation.
11. Support future Azure and Microsoft Entra integration.
12. Provide sufficient documentation for repeatable implementation and troubleshooting.

---

# Design Principles

## Requirements Before Configuration

Virtual network assignments must support documented business, technical, and security requirements.

The design process follows:

**Business Requirement → Technical Requirement → Network Requirement → Design Decision → Implementation → Validation**

Virtual networks will not be created without a documented purpose.

---

## Security by Design

The network architecture will enforce separation between systems based on their functions and security requirements.

Segmentation must support:

- Least-privilege access
- Controlled inter-network communication
- Administrative isolation
- Infrastructure protection
- Security monitoring
- Testing environment isolation
- Troubleshooting
- Future cloud connectivity

The presence of separate networks does not automatically establish secure communication.

Firewall policies must explicitly define which traffic is permitted between network segments.

---

## Documentation First

Virtual networking configurations must be documented before deployment.

Documentation must identify:

- Virtual network name
- VMware network identifier
- Network purpose
- IP subnet
- Default gateway
- Firewall interface
- Connected systems
- DHCP requirements
- DNS requirements
- Security restrictions
- Expected traffic flows

Implementation procedures will be maintained separately from the network design documentation.

---

# Approved Virtualization Platform

Stoneleaf Services will use:

**VMware Workstation Pro**

The initial environment will operate on a single physical Windows host.

VMware Workstation Pro will provide virtual machine execution and virtual networking.

The architecture will use:

- VMware NAT networking for external connectivity.
- Custom VMware host-only networks for internal connectivity.
- pfSense for inter-network routing and firewall enforcement.
- pfSense for internal DHCP services.
- Windows Server for Active Directory Domain Services and internal DNS.
- Ubuntu Server for Linux administration and services.
- Windows workstations for organizational endpoints.
- Dedicated virtual network connectivity for infrastructure, user endpoints, management, and testing.

VMware virtual networking will provide Layer 2 connectivity within each internal network.

pfSense will provide Layer 3 routing between internal networks.

---

# Initial Network Architecture

Stoneleaf Services will initially implement four internal virtual networks.

| Network | Subnet | Gateway | Status |
|---|---|---|---|
| Infrastructure | `10.10.10.0/24` | `10.10.10.1` | Planned |
| User Endpoints | `10.10.20.0/24` | `10.10.20.1` | Planned |
| Management | `10.10.30.0/24` | `10.10.30.1` | Planned |
| Lab / Testing | `10.10.60.0/24` | `10.10.60.1` | Planned |

These networks will remain logically separated within VMware.

Communication between them will be routed through `SLS-FW01`.

---

# Approved VMware Network Model

## Network Assignments

| VMware Network | Type | Function | Subnet |
|---|---|---|---|
| `VMnet8` | NAT | WAN / External Connectivity | VMware-assigned |
| `VMnet2` | Host-Only | Infrastructure | `10.10.10.0/24` |
| `VMnet3` | Host-Only | User Endpoints | `10.10.20.0/24` |
| `VMnet4` | Host-Only | Management | `10.10.30.0/24` |
| `VMnet5` | Host-Only | Lab / Testing | `10.10.60.0/24` |

These assignments are the approved Stoneleaf Services virtual network standard.

The VMware network identifiers must remain consistent throughout the project.

## Internal Network Configuration

For each internal network:

- Use a custom VMware host-only virtual network.
- Configure the appropriate subnet.
- Disable VMware DHCP.
- Disable the host virtual adapter unless specifically required by an approved management procedure.
- Do not enable VMware NAT on internal networks.
- Do not bridge internal networks directly to the physical host network.
- Do not create additional virtual network paths that bypass pfSense.

The initial design does not require IEEE 802.1Q VLAN tagging.

Each internal VMware network functions as a separate virtual Layer 2 segment.

The VMware host must not act as an alternative router between Stoneleaf Services networks.

---

# Virtual Network Architecture

The approved network traffic path is:

**Internal Virtual Machine → Internal VMware Network → SLS-FW01 → Destination Network**

For internet connectivity:

**Internal Virtual Machine → SLS-FW01 → VMnet8 → VMware NAT → Physical Host Network → Internet**

All routed traffic between Stoneleaf Services security zones must traverse pfSense.

VMware NAT will provide upstream connectivity to the physical host network.

The initial design will not expose internal Stoneleaf Services systems directly to the internet.

Double NAT is acceptable for the initial environment.

Future VPN and hybrid-cloud requirements may justify a different WAN configuration, subject to formal design review.

---

# pfSense Network Architecture

## Primary Firewall

Hostname:

`SLS-FW01`

Platform:

pfSense

Primary functions:

- Network boundary enforcement
- Inter-network routing
- Stateful firewall inspection
- Network Address Translation
- DHCP services
- Network traffic logging
- Future VPN connectivity

---

# Approved pfSense Interface Model

The firewall virtual machine will have five virtual network adapters.

| Interface | VMware Network | Security Zone | IP Configuration |
|---|---|---|---|
| WAN | `VMnet8` | External | VMware DHCP |
| LAN | `VMnet2` | Infrastructure | `10.10.10.1/24` |
| OPT1 | `VMnet3` | User Endpoints | `10.10.20.1/24` |
| OPT2 | `VMnet4` | Management | `10.10.30.1/24` |
| OPT3 | `VMnet5` | Lab / Testing | `10.10.60.1/24` |

The interface names above represent planned logical assignments.

Actual virtual NIC identifiers must be verified during deployment.

## WAN Security

The WAN interface will obtain an address from VMware NAT.

Because VMware NAT normally assigns a private IPv4 address, the pfSense WAN configuration must permit the expected upstream private address space.

The VMware NAT subnet must not overlap any Stoneleaf Services internal subnet or the future Azure address space.

Unsolicited inbound WAN traffic will be denied unless an approved requirement authorizes a specific exception.

---

# External Network Connectivity

## WAN Design

The initial Stoneleaf Services WAN connection will use VMware NAT networking.

`SLS-FW01` will receive its WAN configuration through the VMware NAT network.

The expected traffic path is:

**Stoneleaf Internal Network → SLS-FW01 → VMware NAT → Host Network → Internet**

This arrangement provides outbound connectivity without requiring the Stoneleaf Services firewall to connect directly to the physical network as a bridged device.

The initial environment will not require inbound internet access.

Port forwarding and externally accessible services will not be enabled without documented requirements and security review.

VMware NAT and pfSense outbound NAT may result in double NAT.

This is acceptable for the initial learning environment, although it may require additional consideration for future VPN configurations.

The VMware NAT subnet must not overlap the physical host network, any Stoneleaf Services internal subnet, or the reserved Azure address space. The actual WAN subnet, lease, upstream gateway, and DNS settings will be recorded during implementation.

---

# Infrastructure Network

## Network

`10.10.10.0/24`

## VMware Assignment

`VMnet2`

## Default Gateway

`10.10.10.1`

## Purpose

The Infrastructure network provides connectivity for core Stoneleaf Services servers and network services.

Initial systems include:

| System | Address | Function |
|---|---|---|
| `SLS-FW01` | `10.10.10.1` | Infrastructure gateway |
| `SLS-DC01` | `10.10.10.10` | Active Directory and DNS |
| `SLS-LNX01` | `10.10.10.20` | Ubuntu Server |

Infrastructure systems will generally use static IP addresses.

## Security Requirements

Infrastructure systems must not receive unrestricted access from ordinary user or testing networks.

Required services will be permitted through documented firewall policies.

Administrative access should originate from approved management systems whenever practical.

---

# User Endpoint Network

## Network

`10.10.20.0/24`

## VMware Assignment

`VMnet3`

## Default Gateway

`10.10.20.1`

## Purpose

The User Endpoint network provides connectivity for standard organizational workstations.

Initial systems include:

- `SLS-WS01` — Investigations Workstation
- `SLS-WS02` — Intelligence / Analysis Workstation

`SLS-WS03` is assigned exclusively to the Management network on `VMnet4` and is not a User Endpoint network member.

## DHCP

Proposed DHCP range:

`10.10.20.100 – 10.10.20.199`

DHCP services will be provided by pfSense.

Domain-joined workstations will receive the internal DNS server address:

`10.10.10.10`

## Security Requirements

User workstations must be able to access approved infrastructure services.

Typical requirements include:

- DNS
- Active Directory authentication
- Group Policy
- Approved internal resources
- Internet connectivity

Unnecessary administrative access to infrastructure systems must be restricted.

---

# Management Network

## Network

`10.10.30.0/24`

## VMware Assignment

`VMnet4`

## Default Gateway

`10.10.30.1`

## Purpose

The Management network provides a separate security boundary for privileged administrative activities.

Potential management targets include:

- pfSense
- Windows Server
- Ubuntu Server
- Approved guest infrastructure management services
- Future network appliances
- Future storage systems
- Future monitoring infrastructure

## Security Requirements

Management access must be restricted to authorized systems and administrative identities.

Ordinary user workstations must not automatically receive access to management interfaces.

The design follows:

**User Access ≠ Administrative Access**

`SLS-WS03` is the dedicated administrative workstation, connected exclusively to `VMnet4` with static address `10.10.30.10/24`. VMware Workstation Pro itself is administered directly on the physical host as described in Administrative Access to VMware.

---

# Management Workstation Architecture

## Approved Workstation

Hostname:

`SLS-WS03`

Platform:

Windows 11

Function:

Dedicated Infrastructure Administration Workstation

VMware Network:

`VMnet4`

Network:

`10.10.30.0/24`

Static IP Address:

`10.10.30.10`

Default Gateway:

`10.10.30.1`

Primary DNS:

`10.10.10.10`

## Purpose

`SLS-WS03` will serve as the primary administrative workstation for Stoneleaf Services.

It will provide a controlled location for performing privileged infrastructure administration.

Administrative activities may include:

- Windows Server administration
- Active Directory management
- DNS administration
- Group Policy management
- pfSense administration
- Linux server administration
- Network troubleshooting
- Security configuration
- Infrastructure monitoring
- Future Azure administration

## Domain Membership

`SLS-WS03` will be joined to the Stoneleaf Services Active Directory domain.

The workstation will use internal DNS hosted by `SLS-DC01`.

The final Active Directory DNS namespace will be defined in the DNS Design document before domain deployment.

## Administrative Access

Administrative access will be controlled through:

- Dedicated administrative accounts
- Active Directory security groups
- Role-based permissions
- Windows security policies
- Firewall restrictions
- Administrative activity logging

Standard user accounts must not automatically receive privileged administrative access.

Privileged credentials should not be used for routine browsing, email, or ordinary workstation activity.

## Management Network Restrictions

The Management network will be permitted to access approved administrative services on Infrastructure systems.

The User Endpoint network will not be permitted unrestricted access to Management systems.

The Lab / Testing network will be denied access to the Management network by default.

The Management workstation must not provide routing or bridging between security zones.

## Management Workstation Security

`SLS-WS03` must use:

- Windows Defender Firewall
- Endpoint protection
- Security updates
- Account lockout controls
- Least-privilege permissions
- Screen locking
- Administrative logging
- Controlled remote administration

Remote Desktop, PowerShell Remoting, SSH, and other administrative services will be enabled only where justified.

---

# Management Network Addressing

Network:

`10.10.30.0/24`

Gateway:

`10.10.30.1`

| Address | Assignment |
|---|---|
| `10.10.30.1` | `SLS-FW01` Management Gateway |
| `10.10.30.10` | `SLS-WS03` Management Workstation |
| `10.10.30.11 – 10.10.30.49` | Reserved Management Systems |
| `10.10.30.50 – 10.10.30.99` | Reserved Infrastructure Management |
| `10.10.30.100 – 10.10.30.199` | Future DHCP Pool, if required |

The initial Management workstation will use static addressing.

The Management network will not require an active DHCP scope during the initial deployment.

---

# Management Traffic Requirements

| Source | Destination | Function | Policy |
|---|---|---|---|
| `SLS-WS03` | `SLS-DC01` | DNS / Active Directory | Allow required services |
| `SLS-WS03` | `SLS-DC01` | Windows Administration | Allow approved services |
| `SLS-WS03` | `SLS-LNX01` | SSH Administration | Allow |
| `SLS-WS03` | `SLS-FW01` | HTTPS Administration | Allow |
| `SLS-WS03` | Internet | Updates / Approved Resources | Restricted |
| User Endpoints | Management | Unapproved Administrative Access | Deny |
| Lab / Testing | Management | Unapproved Access | Deny |

Specific ports, protocols, directions, and firewall rules will be defined in:

`09-Firewall-Policy-Matrix.md`

---

# Administrative Access to VMware

VMware Workstation Pro operates on the physical virtualization host.

Administration of the VMware application, virtual machine files, and virtual networking configuration will initially occur directly on the physical host.

`SLS-WS03` will not be treated as a remote VMware management console unless a supported and documented remote management mechanism is introduced.

The physical host and Stoneleaf Services virtual management network are separate administrative environments.

Access to the physical host must be protected through the host operating system's security controls.

---

# Lab / Testing Network

## Network

`10.10.60.0/24`

## VMware Assignment

`VMnet5`

## Default Gateway

`10.10.60.1`

## Purpose

The Lab / Testing network provides an isolated environment for temporary systems, troubleshooting, experimentation, and training.

Potential systems include:

- Temporary Windows virtual machines
- Temporary Linux virtual machines
- Test servers
- Security training systems
- Vulnerable training systems
- Network troubleshooting systems
- Experimental applications

## Security Requirements

The Lab / Testing network must not receive unrestricted access to normal Stoneleaf Services infrastructure.

Access to the Infrastructure and Management networks should be denied unless a documented requirement explicitly permits a connection.

Internet access may be provided for software installation, updates, and approved training activities.

Higher-risk testing systems may require additional isolation, including temporary removal of internet access.

---

# Approved Virtual Machine Placement

| Virtual Machine | Function | VMware Network | IP Address |
|---|---|---|---|
| `SLS-FW01` | Firewall | `VMnet8`, `VMnet2`, `VMnet3`, `VMnet4`, `VMnet5` | Multiple |
| `SLS-DC01` | Active Directory / DNS | `VMnet2` | `10.10.10.10` |
| `SLS-LNX01` | Linux Server | `VMnet2` | `10.10.10.20` |
| `SLS-WS01` | Investigations Workstation | `VMnet3` | DHCP |
| `SLS-WS02` | Intelligence / Analysis Workstation | `VMnet3` | DHCP |
| `SLS-WS03` | Management Workstation | `VMnet4` | `10.10.30.10` |

Each server and workstation will initially use one virtual network adapter.

Only `SLS-FW01` will connect directly to multiple Stoneleaf Services security zones.

Additional network adapters must not be added without a documented technical requirement.

The Lab / Testing network will initially exist even if no permanent testing systems are assigned to it. Additional virtual machines will be introduced only for documented project objectives.

---

# VLAN Architecture

## Initial VLAN Requirements

The initial Stoneleaf Services environment will not require IEEE 802.1Q VLAN tagging.

Segmentation will be provided through separate VMware virtual networks connected to individual pfSense interfaces.

This approach allows Stoneleaf Services to implement:

- Separate network boundaries
- Inter-network routing
- Firewall enforcement
- Controlled communication
- Administrative isolation
- Testing isolation

without requiring physical VLAN-capable networking equipment.

The VMware network identifiers are not VLAN IDs.

For example:

`VMnet2` does not represent VLAN 2.

---

# Future Physical VLAN Design

Stoneleaf Services may introduce IEEE 802.1Q VLAN tagging when physical networking infrastructure is added.

The following VLAN identifiers are reserved for future use:

| VLAN ID | Network | Subnet | Status |
|---|---|---|---|
| 10 | Infrastructure | `10.10.10.0/24` | Future |
| 20 | User Endpoints | `10.10.20.0/24` | Future |
| 30 | Management | `10.10.30.0/24` | Future |
| 40 | Security Operations | `10.10.40.0/24` | Reserved |
| 50 | Investigations | `10.10.50.0/24` | Reserved |
| 60 | Lab / Testing | `10.10.60.0/24` | Future |
| 70 | Storage / Backup | `10.10.70.0/24` | Reserved |
| 80 | Network Infrastructure | `10.10.80.0/24` | Reserved |

These VLAN IDs are reserved design values and will not be configured during the initial deployment. Reserved future networks do not require additional pfSense adapters or active VMware segments in the initial five-NIC design.

## Future VLAN Implementation

A future physical deployment may require:

- Managed switches
- VLAN-capable network adapters
- Tagged trunk connections
- Access-port assignments
- pfSense VLAN interfaces
- Updated VMware networking
- Revised firewall interface assignments
- Updated network diagrams
- Validation of inter-VLAN routing

The existing IP addressing scheme should remain unchanged where practical.

Any transition to physical VLANs must follow Stoneleaf Services change-management procedures.

---

# DHCP Architecture

pfSense will provide DHCP services for applicable Stoneleaf Services networks.

VMware DHCP must remain disabled on internal virtual networks to prevent competing DHCP services.

The initial DHCP design will support:

- Dynamic workstation addressing
- Correct default gateway assignment
- Internal DNS assignment
- Network-specific DHCP scopes
- Address reservations where required

Critical infrastructure systems will generally use static addresses.

Detailed DHCP configurations will be defined in:

`06-DHCP-Design.md`

The initial User Endpoint DHCP scope is planned as `10.10.20.100 – 10.10.20.199`. Infrastructure servers and `SLS-WS03` use static addresses. No Management DHCP scope will be active initially; `10.10.30.100 – 10.10.30.199` is reserved for a future scope if required. Lab / Testing DHCP scope details and any infrastructure DHCP requirement must be defined in `06-DHCP-Design.md` before activation. VMware DHCP on `VMnet8` remains available for the pfSense WAN lease; disabling VMware DHCP applies to the four internal VMnets.

---

# DNS Architecture

`SLS-DC01` will provide internal DNS services for the Stoneleaf Services Active Directory environment.

Primary internal DNS server:

`10.10.10.10`

Domain-joined systems must use the appropriate internal DNS service.

The DNS architecture must support:

- Active Directory
- Domain joining
- Internal hostname resolution
- Authentication
- Group Policy
- External name resolution
- Future cloud integration

The final internal DNS namespace and forwarding configuration will be established in:

`07-DNS-Design.md`

---

# Routing Architecture

`SLS-FW01` will provide routing between the initial Stoneleaf Services networks.

Each internal network will use its corresponding pfSense interface as the default gateway.

Inter-network routing must be subject to firewall policy.

Direct communication between separate VMware virtual networks must not bypass the firewall.

Detailed routing and NAT requirements will be documented in:

`08-Routing-and-NAT-Design.md`

---

# Firewall Architecture

Network segmentation must be supported by explicit firewall rules.

The firewall design will define:

- Allowed network traffic
- Denied network traffic
- Administrative access
- DNS and Active Directory connectivity
- Internet access
- Testing environment restrictions
- Logging requirements
- Future VPN connectivity

Firewall rules must follow least-privilege principles.

Specific rules, ports, protocols, and destinations will be documented in:

`09-Firewall-Policy-Matrix.md`

---

# Network Security Requirements

The initial VMware network architecture must enforce:

1. Separation of Infrastructure and User Endpoints.
2. Dedicated Management network connectivity.
3. Isolation of Lab / Testing systems.
4. Centralized inter-network routing through pfSense.
5. Controlled administrative access.
6. Internal DNS for domain-joined systems.
7. Approved internet access.
8. Firewall logging.
9. Protection against unintended host-based network bypasses.
10. Denial of unnecessary inter-network communication.

All required network communications must be explicitly documented.

---

# Network Traffic Flows

Important traffic flows must be documented before implementation.

Initial traffic flows include:

| Source | Destination | Purpose |
|---|---|---|
| User Endpoints | Infrastructure | DNS and Active Directory |
| User Endpoints | WAN | Approved internet access |
| Management | Infrastructure | Authorized administration |
| Management | pfSense | Firewall administration |
| Infrastructure | WAN | Updates and approved services |
| Lab / Testing | WAN | Approved testing and updates |
| Lab / Testing | Infrastructure | Denied by default |
| Lab / Testing | Management | Denied by default |
| User Endpoints | Management | Denied unless explicitly authorized |

Required Active Directory communication must account for the relevant protocols and ports.

Detailed traffic requirements will be maintained in:

`10-Network-Traffic-Flow-Matrix.md`

---

# Future Network Expansion

The following networks remain reserved:

| Network | Subnet | Status |
|---|---|---|
| Security Operations | `10.10.40.0/24` | Reserved |
| Investigations | `10.10.50.0/24` | Reserved |
| Storage / Backup | `10.10.70.0/24` | Reserved |
| Network Infrastructure | `10.10.80.0/24` | Reserved |

Additional networks must not be activated without documented requirements.

New virtual networks must include:

- Defined purpose
- Addressing plan
- Gateway assignment
- Firewall interface
- DHCP requirements
- DNS requirements
- Security policy
- Traffic-flow documentation
- Validation procedures

---

# Future Azure Integration

Stoneleaf Services reserves the following address space for future Microsoft Azure networking:

`10.20.0.0/16`

This address space must remain separate from the on-premises Stoneleaf Services address space:

`10.10.0.0/16`

Future hybrid connectivity may require:

- Azure virtual networks
- Azure subnets
- VPN connectivity
- Routing configuration
- Firewall policy updates
- DNS integration
- Microsoft Entra integration
- Network monitoring

The VMware and pfSense network architecture must support future hybrid connectivity without unnecessary redesign.

Detailed cloud implementation requirements will be maintained in the Azure and Microsoft Entra project documentation.

---

# Implementation Dependencies

Before deploying the network, Stoneleaf Services must confirm:

- VMware Workstation Pro version and compatibility.
- Physical host hardware resources.
- Support for five pfSense virtual network adapters.
- VMware virtual network availability.
- VMware NAT subnet selection.
- Absence of overlapping host, on-premises, and Azure address ranges.
- pfSense compatibility with the selected virtual network adapters.
- Required Windows and Linux installation media.
- Approved IP addressing.
- Approved DNS architecture.
- Approved firewall traffic requirements.
- Availability of a recovery method if administrative access is lost.

The virtual network design must be approved before implementation begins.

---

# Network Validation Requirements

The virtual network architecture must be validated after implementation.

Validation must confirm:

1. Each virtual machine is connected to the correct VMware network.
2. pfSense interfaces have the correct network assignments.
3. Internal networks use the documented gateways.
4. VMware DHCP does not conflict with pfSense DHCP.
5. User workstations receive appropriate network configuration.
6. Internal DNS resolution functions correctly.
7. Domain-joined workstations can reach required Active Directory services.
8. Approved traffic can cross network boundaries.
9. Unauthorized traffic is blocked.
10. Lab / Testing systems cannot bypass intended security boundaries.
11. Authorized systems can access the internet.
12. Firewall logging records relevant network activity.
13. Network connectivity can be systematically troubleshot.
14. The environment can be rebuilt using documented implementation procedures.

Detailed test procedures and acceptance criteria will be maintained in:

`12-Network-Validation-and-Test-Plan.md`

## VMware and Management Validation

1. `VMnet8` provides WAN connectivity.
2. `VMnet2` provides Infrastructure connectivity.
3. `VMnet3` provides User Endpoint connectivity.
4. `VMnet4` provides Management connectivity.
5. `VMnet5` provides Lab / Testing connectivity.
6. VMware DHCP is disabled on internal networks.
7. pfSense is the gateway for all internal networks.
8. `SLS-WS03` receives the approved static IP configuration.
9. `SLS-WS03` resolves internal DNS records.
10. `SLS-WS03` can authenticate to Active Directory.
11. `SLS-WS03` can reach approved administrative services.
12. Ordinary workstations cannot access unauthorized management services.
13. Lab / Testing systems cannot access restricted Management systems.
14. Internal systems can access approved external services.
15. Inter-network traffic follows the documented firewall policies.
16. The physical host does not provide an unintended routing bypass.

Each test must record its expected result, actual result, date, configuration evidence, and pass/fail status. Unexecuted tests remain Not Tested; this document reports no successful deployment or validation.

---

# Implementation Documentation

The Network Design phase defines the intended architecture.

Detailed deployment procedures will be maintained separately in the Stoneleaf Services implementation playbooks.

Implementation documentation must include:

- Prerequisites
- Software versions
- Virtual machine requirements
- Network adapter assignments
- Configuration procedures
- Commands and settings
- Expected results
- Verification steps
- Screenshots and evidence
- Troubleshooting procedures
- Rollback procedures
- Change records

The implementation playbooks must allow the environment to be recreated from a clean starting point.

---

# Change Management

Changes to the virtual networking architecture must be documented.

Changes requiring review include:

- Adding or removing virtual networks
- Changing VMware network assignments
- Changing IP subnets
- Modifying pfSense interfaces
- Introducing VLAN tagging
- Changing network gateways
- Changing routing behavior
- Modifying DHCP architecture
- Introducing new security zones
- Changing connectivity to external networks

Approved changes must be reflected in all affected design documents, diagrams, implementation procedures, and validation records.

---

# Design Decisions

## DD-NET-001 — VMware Network Model

**Decision:** Use VMware Workstation Pro custom host-only networks for internal segmentation and VMware NAT for WAN connectivity.

**Reason:** Provides practical network isolation and routing exercises without requiring physical managed switches.

**Status:** Approved for Initial Design

## DD-NET-002 — Routing and Firewall Platform

**Decision:** Use `SLS-FW01` as the primary router and firewall for all internal Stoneleaf Services networks.

**Reason:** Provides centralized policy enforcement, routing, NAT, and troubleshooting.

**Status:** Approved for Initial Design

## DD-NET-003 — Management Workstation Placement

**Decision:** Place `SLS-WS03` exclusively on `VMnet4`, using `10.10.30.10/24`.

**Reason:** Separates privileged administration from standard organizational endpoint activity.

**Status:** Approved for Initial Design

## DD-NET-004 — Initial VLAN Strategy

**Decision:** Do not implement 802.1Q VLAN tagging during the initial single-host deployment.

**Reason:** Separate VMware virtual networks already provide the required initial segmentation.

**Status:** Approved for Initial Design

---

# Completion Criteria

The VLAN and Virtual Network Design phase will be considered ready for implementation when:

- VMware Workstation Pro and all five VMware virtual networks are defined.
- Each network has a documented purpose.
- Network addressing matches the approved IP Addressing Plan.
- pfSense interface assignments are documented.
- Virtual machine network placement is documented, including `SLS-WS03` exclusively on `VMnet4` at `10.10.30.10/24`.
- DHCP and DNS responsibilities are defined.
- Routing requirements are identified.
- Security boundaries are established.
- Required traffic flows are identified.
- Future VLAN expansion is documented.
- Validation requirements are established.
- Implementation dependencies are identified.

Design readiness is separate from operational completion. The approved architecture remains **Planned — Pending Implementation** until deployed. Implementation completion and validation acceptance must be tracked separately and supported by evidence.

---

# Document Status

**Project:** Stoneleaf Services

**Document:** 05 — VLAN and Virtual Network Design

**Phase:** Network Design

**Status:** Approved Design — Pending Implementation

**Implementation Status:** Not Started

**Validation Status:** Not Tested

**Next Document:** `06-DHCP-Design.md`

