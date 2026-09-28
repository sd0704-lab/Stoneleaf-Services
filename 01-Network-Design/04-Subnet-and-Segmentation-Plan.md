# Stoneleaf Services — Subnet and Segmentation Plan

**No Stone Left Unturned**

## Purpose

This document defines the subnet and network segmentation architecture for the Stoneleaf Services environment.

The IP Addressing Plan established the following primary address spaces:

- Stoneleaf On-Premises: `10.10.0.0/16`
- Future Microsoft Azure: `10.20.0.0/16`

This document determines which on-premises networks will be implemented initially, which networks will remain reserved for future use, and why systems are separated into different network security zones.

The objective is to provide meaningful security and administrative separation without introducing unnecessary complexity.

---

# Design Philosophy

Stoneleaf Services uses functional and security-based segmentation.

Network segments will not automatically correspond to organizational departments.

The existence of departments such as:

- Executive Leadership
- Information Technology
- Cybersecurity
- Digital Investigations
- Intelligence & Analysis
- Business Operations
- Project & Client Services
- Legal & Compliance

does not mean that each department requires its own subnet or VLAN.

Identity-based access will primarily be controlled through:

- Active Directory
- Security groups
- Resource permissions
- Group Policy
- Authentication
- Authorization
- Endpoint security

Network segmentation provides an additional security boundary where separation provides a technical or operational benefit.

---

# Segmentation Objectives

Stoneleaf Services segmentation must:

1. Separate core infrastructure from ordinary endpoints.
2. Provide a protected path for administrative activity.
3. Isolate experimental and testing systems from normal infrastructure.
4. Support future security operations.
5. Support future digital investigation environments.
6. Support future centralized storage.
7. Support future physical network infrastructure.
8. Permit controlled communication between networks.
9. Support firewall enforcement.
10. Support logging and monitoring.
11. Improve troubleshooting.
12. Support future Azure connectivity.
13. Remain practical for a home-lab environment.
14. Avoid unnecessary complexity.

---

# Segmentation Model

The Stoneleaf Services on-premises address space is:

`10.10.0.0/16`

Individual functional networks will generally use:

`/24`

subnets.

The initial design contains two categories:

- **Implemented Networks**
- **Reserved Networks**

Implemented networks will be created during the initial Stoneleaf deployment.

Reserved networks have assigned address space but will not necessarily be created until a documented requirement exists.

---

# Initial Implemented Networks

The initial Stoneleaf Services environment will implement four functional networks:

| Network | Subnet | Gateway | Initial Status |
| --- | --- | --- | --- |
| Infrastructure | `10.10.10.0/24` | `10.10.10.1` | Implement |
| User Endpoints | `10.10.20.0/24` | `10.10.20.1` | Implement |
| Management | `10.10.30.0/24` | `10.10.30.1` | Implement |
| Lab / Testing | `10.10.60.0/24` | `10.10.60.1` | Implement |

These networks provide meaningful segmentation for the initial environment without requiring every reserved security zone to be deployed immediately.

---

# Reserved Networks

The following networks remain reserved for future deployment:

| Network | Subnet | Gateway | Status |
| --- | --- | --- | --- |
| Security Operations | `10.10.40.0/24` | `10.10.40.1` | Reserved |
| Investigations | `10.10.50.0/24` | `10.10.50.1` | Reserved |
| Storage / Backup | `10.10.70.0/24` | `10.10.70.1` | Reserved |
| Network Infrastructure | `10.10.80.0/24` | `10.10.80.1` | Reserved |

These networks will be implemented when actual systems or requirements justify their use.

---

# Infrastructure Network

## Network

`10.10.10.0/24`

## Gateway

`10.10.10.1`

## Purpose

The Infrastructure network contains systems that provide core services to the Stoneleaf Services environment.

Initial systems include:

- `SLS-DC01`
- `SLS-LNX01`

Future systems may include:

- File servers
- Application servers
- Internal service servers
- Additional domain controllers
- Logging infrastructure
- Monitoring infrastructure

---

# Infrastructure Addressing

Initial static assignments include:

| System | Address |
| --- | --- |
| Gateway | `10.10.10.1` |
| `SLS-DC01` | `10.10.10.10` |
| `SLS-LNX01` | `10.10.10.20` |

Infrastructure systems will generally use predictable static addressing.

---

# Infrastructure Security Objective

Infrastructure systems should not be treated as equivalent to ordinary user endpoints.

The network boundary allows Stoneleaf Services to control which systems may communicate with infrastructure services.

Required communication may include:

- DNS
- Active Directory
- Authentication
- Group Policy
- Administrative access
- Linux administration
- Logging
- Monitoring

Unnecessary access can be restricted through firewall policy.

---

# User Endpoint Network

## Network

`10.10.20.0/24`

## Gateway

`10.10.20.1`

## Purpose

The User Endpoint network contains normal organizational workstations.

Initial systems include:

- `SLS-WS01`
- `SLS-WS02`
- `SLS-WS03`

These systems represent:

- Investigations
- Intelligence / Analysis
- Management / Administration

Their organizational roles do not automatically require separate network segments during the initial deployment.

---

# User Endpoint Addressing

The planned DHCP range is:

`10.10.20.100 – 10.10.20.199`

Workstations will generally receive their network configuration through DHCP.

Final DHCP configuration will be documented in:

`06-DHCP-Design.md`

---

# User Endpoint Security Objective

User endpoints require access to selected infrastructure services but should not receive unrestricted access to every infrastructure resource.

Typical required communication includes:

- DHCP
- DNS
- Active Directory
- Authentication
- Group Policy
- Approved internal services
- Internet access

Specific traffic permissions will be defined in the Traffic Flow Matrix and Firewall Architecture documents.

---

# Management Network

## Network

`10.10.30.0/24`

## Gateway

`10.10.30.1`

## Purpose

The Management network provides a dedicated security boundary for infrastructure administration.

This network separates administrative activity from ordinary user traffic.

Potential management targets include:

- `SLS-FW01`
- `SLS-DC01`
- `SLS-LNX01`
- VMware
- Future servers
- Future managed switches
- Future wireless infrastructure
- Future storage systems
- Future security infrastructure

---

# Management Security Objective

The Management network should become the preferred origin for privileged infrastructure administration.

Ordinary user endpoints should not automatically receive unrestricted access to management interfaces.

The design supports the principle:

**User Access ≠ Administrative Access**

Administrative privileges and administrative network access are separate controls.

---

# Initial Management Implementation

The Management network will be created during the initial deployment even if only a limited number of systems initially use it.

This provides an environment for learning and implementing:

- Administrative isolation
- Firewall policy
- Multi-network routing
- Management access control
- Troubleshooting across security zones
- Least-privilege network design

`SLS-WS03` may initially function as the administrative workstation.

Its final network placement will be determined during VMware and firewall implementation.

A future dedicated administrative workstation may be introduced if required.

---

# Lab / Testing Network

## Network

`10.10.60.0/24`

## Gateway

`10.10.60.1`

## Purpose

The Lab / Testing network provides an isolated environment for temporary and experimental systems.

Potential systems include:

- Temporary virtual machines
- Training systems
- Troubleshooting systems
- Test servers
- Temporary Linux systems
- Temporary Kali Linux systems
- Vulnerable training machines
- Experimental configurations
- Security testing systems

---

# Lab / Testing Security Objective

Lab systems should not automatically receive the same level of trust as normal Stoneleaf Services systems.

The Lab / Testing network must support stronger isolation from:

- Infrastructure
- Management
- Sensitive future networks
- Storage
- Investigation systems

Access will be explicitly allowed when required.

---

# Lab / Testing Internet Access

Lab systems may require internet access for:

- Updates
- Package repositories
- Software installation
- Training
- Research

Internet access may therefore be permitted through `SLS-FW01` while internal access remains more restrictive.

Exact firewall policy will be defined later.

---

# Security Operations Network

## Network

`10.10.40.0/24`

## Status

**Reserved**

## Purpose

This network is reserved for future cybersecurity infrastructure.

Potential systems include:

- SIEM
- Log collectors
- Security monitoring
- Detection systems
- Vulnerability-management systems
- Security-analysis systems
- Security automation systems

---

# Security Operations Activation Criteria

The Security Operations network should be implemented when Stoneleaf Services deploys dedicated security infrastructure requiring protected access to multiple network zones.

Until then:

`10.10.40.0/24`

remains reserved.

---

# Investigations Network

## Network

`10.10.50.0/24`

## Status

**Reserved**

## Purpose

This network is reserved for future digital investigation infrastructure.

Potential systems include:

- Forensic workstations
- Evidence-processing systems
- Investigation servers
- Evidence repositories
- Incident-analysis systems
- Specialized investigation environments

---

# Investigations Activation Criteria

The Investigations network should be implemented when Stoneleaf Services introduces dedicated investigation infrastructure requiring stronger isolation than the standard User Endpoint network.

Until then, `SLS-WS01` may operate on the User Endpoint network.

`10.10.50.0/24`

remains reserved.

---

# Storage / Backup Network

## Network

`10.10.70.0/24`

## Status

**Reserved**

## Purpose

This network is reserved for future centralized storage and backup infrastructure.

Potential systems include:

- NAS
- Backup server
- VM backup repository
- Security-log storage
- Documentation storage
- Investigation storage

---

# Storage Activation Criteria

The Storage / Backup network should be implemented when centralized network storage is introduced and a dedicated security or traffic boundary provides a documented benefit.

Until then:

`10.10.70.0/24`

remains reserved.

---

# Network Infrastructure Network

## Network

`10.10.80.0/24`

## Status

**Reserved**

## Purpose

This network is reserved for future physical network infrastructure.

Potential devices include:

- Managed switches
- Wireless access points
- Network controllers
- Additional network appliances

---

# Network Infrastructure Activation Criteria

This network should be implemented when Stoneleaf Services expands into physical managed network infrastructure and a dedicated infrastructure-management segment becomes useful.

Until then:

`10.10.80.0/24`

remains reserved.

---

# Initial Segmentation Diagram

The initial segmentation architecture is:

    Internet
       |
       |
    Home Network
       |
       |
    VMware Host
       |
       |
    SLS-FW01
      pfSense
       |
       +-------------------------------------------+
       |              |              |             |
       |              |              |             |
    Infrastructure   Users       Management     Lab / Test
    10.10.10.0/24  10.10.20.0/24 10.10.30.0/24 10.10.60.0/24
       |              |              |             |
    SLS-DC01       SLS-WS01      Admin Access   Temporary VMs
    SLS-LNX01      SLS-WS02                     Test Systems
                   SLS-WS03*                    Training Systems

`SLS-WS03` placement may change when the Management architecture is finalized.

---

# Future Segmentation Diagram

The architecture can later expand to:

    SLS-FW01
       |
       +--------------------------------------------------------------+
       |        |         |         |         |         |       |     |
       |        |         |         |         |         |       |     |
     INFRA     USER      MGMT      SECOPS     INVEST    LAB   STORAGE NET-INFRA
       |        |         |         |         |         |       |     |
      .10      .20       .30       .40       .50       .60     .70   .80

Where:

- `.10` = Infrastructure
- `.20` = User Endpoints
- `.30` = Management
- `.40` = Security Operations
- `.50` = Investigations
- `.60` = Lab / Testing
- `.70` = Storage / Backup
- `.80` = Network Infrastructure

Each represents the third octet of its corresponding `10.10.X.0/24` subnet.

---

# Inter-Segment Routing

`SLS-FW01` will provide routing between implemented Stoneleaf Services networks.

This means traffic moving between:

- Infrastructure
- User Endpoints
- Management
- Lab / Testing
- Future security zones

will pass through pfSense when the architecture is implemented as designed.

This provides a central point for:

- Routing
- Access control
- Logging
- Monitoring
- Troubleshooting

---

# Inter-Segment Security Model

The existence of a route does not imply permission to communicate.

The design follows:

**Routing provides a path.**

**Firewall policy determines whether traffic may use that path.**

Inter-segment traffic will therefore be controlled through `SLS-FW01`.

---

# High-Level Communication Requirements

## User Endpoints → Infrastructure

**Default:** Restricted / Required Services Allowed

Users will require selected infrastructure services such as:

- DNS
- Active Directory
- Authentication
- Group Policy
- Approved internal services

Unnecessary access should be restricted.

---

## User Endpoints → Management

**Default:** Deny

Ordinary endpoint traffic should not require access to infrastructure-management interfaces.

Exceptions must have a documented administrative requirement.

---

## User Endpoints → Lab / Testing

**Default:** Restricted

Communication may be allowed for approved training or testing scenarios.

Unrestricted access is not required.

---

## Management → Infrastructure

**Default:** Authorized Administrative Access

The Management network requires controlled access to infrastructure systems for administration.

Access should remain limited to authorized administrative services.

---

## Management → User Endpoints

**Default:** Restricted / Administrative Services as Required

Authorized administrators may require remote-management capabilities.

Only required management traffic should be allowed.

---

## Management → Lab / Testing

**Default:** Restricted / Administrative Access as Required

Administrators may require access to test systems for configuration and troubleshooting.

---

## Lab / Testing → Infrastructure

**Default:** Deny

Lab systems should not automatically access protected infrastructure.

Specific exceptions may be created for controlled exercises.

---

## Lab / Testing → Management

**Default:** Deny

Lab systems should not initiate normal connections into the Management network.

---

## Lab / Testing → User Endpoints

**Default:** Deny

Testing systems should not automatically communicate with normal organizational endpoints.

Specific exercises may temporarily require controlled exceptions.

---

## Lab / Testing → Internet

**Default:** Allow as Required

Lab systems may require controlled internet access for updates, software installation, training, and research.

Specific policy will be determined during firewall design.

---

# Initial Policy Matrix

| Source | Destination | High-Level Policy |
| --- | --- | --- |
| User | Infrastructure | Required Services Only |
| User | Management | Deny |
| User | Lab / Testing | Restricted |
| Management | Infrastructure | Authorized Administrative Access |
| Management | User | Required Administrative Services |
| Management | Lab / Testing | Required Administrative Services |
| Lab / Testing | Infrastructure | Deny by Default |
| Lab / Testing | User | Deny by Default |
| Lab / Testing | Management | Deny |
| Infrastructure | User | Required Services Only |
| Internal Networks | Internet | Controlled Outbound Access |

This matrix represents architectural intent.

It does not define individual firewall rules.

Specific ports, protocols, sources, destinations, and rule order will be documented in later documents.

---

# East-West Traffic

Traffic between Stoneleaf Services internal networks is considered east-west traffic.

Examples include:

- User → Infrastructure
- Management → Infrastructure
- Management → User
- Lab → Infrastructure

Where practical, east-west traffic crossing security boundaries should pass through `SLS-FW01`.

This allows firewall policy to control communication between zones.

---

# North-South Traffic

Traffic entering or leaving the Stoneleaf Services environment is considered north-south traffic.

Examples include:

- User → Internet
- Infrastructure → Internet
- Lab → Internet
- Future Azure → On-Premises
- Future On-Premises → Azure

`SLS-FW01` will serve as the primary control point for this traffic.

---

# Broadcast Domains

Each implemented subnet will represent a separate Layer 3 network and broadcast domain.

This provides:

- Traffic separation
- Easier troubleshooting
- Security boundaries
- Reduced unnecessary broadcast propagation
- Clear network identification

VLAN implementation will be defined in:

`05-VLAN-Design.md`

---

# Segmentation and Active Directory

Network segmentation must not prevent required Active Directory communication.

Domain-joined systems require access to services provided by `SLS-DC01`.

Firewall policy must therefore permit required domain traffic from authorized networks.

The exact required ports and protocols will be documented in:

`12-Traffic-Flow-Matrix.md`

and translated into firewall policy later.

---

# Segmentation and DNS

Stoneleaf Services domain clients will use:

`SLS-DC01`

at:

`10.10.10.10`

for internal DNS.

Therefore, authorized client networks must be capable of reaching:

`10.10.10.10`

for DNS services.

Clients should not bypass the internal DNS architecture by using public DNS directly unless a specific exception is documented.

---

# Segmentation and DHCP

pfSense will provide DHCP for networks requiring dynamic addressing.

Each DHCP-enabled network will require a scope appropriate to that subnet.

For example:

User Endpoint Network:

`10.10.20.100 – 10.10.20.199`

DHCP design will be documented separately.

---

# Segmentation and Security Monitoring

Future security infrastructure may require visibility into multiple network segments.

When the Security Operations network is activated, it may require controlled communication with:

- Infrastructure
- User Endpoints
- Management
- Investigations
- Lab / Testing
- Storage
- Network Infrastructure

Monitoring requirements do not imply unrestricted access.

Traffic permissions must be based on the specific monitoring function.

---

# Segmentation and Investigations

Future investigation systems may require:

- Access to evidence sources
- Access to logs
- Controlled internet access
- Access to storage
- Security-event information
- Isolated analysis environments

The Investigation network will be activated when these requirements justify a dedicated network boundary.

---

# Segmentation and Storage

Future storage may contain sensitive data from multiple organizational functions.

Potential examples include:

- Backups
- Security logs
- Investigation evidence
- Technical documentation
- VM backups

Access to storage should therefore be based on authenticated services and documented requirements rather than unrestricted network connectivity.

---

# Segmentation and Azure

Future Azure networks will use address space within:

`10.20.0.0/16`

On-premises Stoneleaf networks use:

`10.10.0.0/16`

The non-overlapping design supports future routed hybrid connectivity.

Future Azure networks should also use functional segmentation where appropriate.

The Azure design does not need to duplicate the on-premises segmentation structure exactly.

---

# VMware Implementation Consideration

The initial segmentation architecture must be reproducible inside VMware.

The VMware design must provide logical connectivity for:

- Infrastructure
- User Endpoints
- Management
- Lab / Testing

while routing inter-network communication through `SLS-FW01`.

VMware network mappings will be established in:

`11-VMware-Network-Design.md`

---

# Why Four Networks Are Implemented Initially

Stoneleaf Services could technically create all eight reserved networks immediately.

Doing so would provide little benefit because several networks would initially contain no systems.

The four initial networks provide immediate educational and technical value.

## Infrastructure

Demonstrates server isolation and controlled service access.

## User Endpoints

Represents normal organizational client systems.

## Management

Demonstrates privileged administrative isolation.

## Lab / Testing

Provides a safer environment for experiments and security exercises.

Together, these four networks provide enough complexity to practice:

- Subnetting
- Routing
- DHCP
- DNS
- Firewall policy
- Network segmentation
- Administrative access
- Troubleshooting
- Security validation

without creating unnecessary empty networks.

---

# Why /24 Networks Are Used

The Stoneleaf Services lab does not require 254 hosts per network.

The `/24` structure is intentionally selected for clarity rather than address conservation.

Benefits include:

- Easy subnet recognition
- Simple troubleshooting
- Simple documentation
- Predictable gateways
- Easy expansion
- Reduced subnetting mistakes
- Clear relationship between function and third octet

The private `10.10.0.0/16` address space provides sufficient capacity for this approach.

---

# Segmentation Security Principle

Network segmentation is one layer of security.

Stoneleaf Services will combine segmentation with:

- Identity
- Authentication
- Authorization
- Active Directory security groups
- Group Policy
- Host firewalls
- pfSense firewall rules
- Least privilege
- Logging
- Monitoring
- Patch management
- Endpoint security

No individual control is treated as sufficient by itself.

---

# Troubleshooting Benefits

Functional segmentation improves troubleshooting because the source and destination networks provide immediate context.

For example:

`10.10.20.125 → 10.10.10.10`

indicates:

**User Endpoint → Infrastructure**

while:

`10.10.60.115 → 10.10.10.10`

indicates:

**Lab / Testing → Infrastructure**

This allows administrators to evaluate:

1. Source configuration
2. Source subnet
3. Source gateway
4. Routing
5. Firewall policy
6. Destination subnet
7. Destination host
8. Destination service

in a systematic order.

---

# Implementation Status

## Initial Deployment

The following networks are approved for initial implementation:

- `10.10.10.0/24` — Infrastructure
- `10.10.20.0/24` — User Endpoints
- `10.10.30.0/24` — Management
- `10.10.60.0/24` — Lab / Testing

## Reserved

The following remain reserved:

- `10.10.40.0/24` — Security Operations
- `10.10.50.0/24` — Investigations
- `10.10.70.0/24` — Storage / Backup
- `10.10.80.0/24` — Network Infrastructure

---

# Design Decisions Established

This document establishes:

1. Functional rather than department-based segmentation.
2. Four networks will be implemented initially.
3. Infrastructure uses `10.10.10.0/24`.
4. User Endpoints use `10.10.20.0/24`.
5. Management uses `10.10.30.0/24`.
6. Lab / Testing uses `10.10.60.0/24`.
7. Security Operations remains reserved at `10.10.40.0/24`.
8. Investigations remains reserved at `10.10.50.0/24`.
9. Storage / Backup remains reserved at `10.10.70.0/24`.
10. Network Infrastructure remains reserved at `10.10.80.0/24`.
11. pfSense will route between implemented networks.
12. pfSense will enforce policy between network security zones.
13. User access and administrative access will be treated separately.
14. Lab systems will be considered lower-trust systems.
15. Lab access to protected internal networks will be denied by default.
16. Network segmentation will complement rather than replace identity-based security.
17. Reserved networks will be activated only when a documented requirement exists.

---

# Decisions Still Pending

The following remain to be defined:

- VLAN IDs
- VLAN names
- VLAN-to-subnet mappings
- VMware virtual network mappings
- Exact pfSense interfaces
- DHCP scopes for each applicable network
- Exact DNS configuration
- Routing configuration
- NAT configuration
- Individual firewall rules
- Required ports and protocols
- Final `SLS-WS03` placement
- Future Security Operations activation
- Future Investigation network activation
- Future Storage network activation
- Future Network Infrastructure activation

---

# Validation Criteria

The segmentation design is considered valid if:

- Core infrastructure is separated from ordinary endpoints.
- Administrative activity can be isolated.
- Test systems can be isolated from protected systems.
- Required Active Directory communication can be permitted.
- Required DNS communication can be permitted.
- Internet access can be controlled.
- Inter-network communication can be filtered.
- Additional security zones can be added without renumbering existing networks.
- The design can be implemented through VMware and pfSense.
- The architecture remains understandable and practical to troubleshoot.
- Each implemented segment has a documented purpose.

---

# Current Status

**Document:** Subnet and Segmentation Plan  
**Phase:** `01-Network-Design`  
**Version:** 1.0  
**Status:** Complete for Initial Design  
**Deployment:** Not Started

The initial Stoneleaf Services segmentation architecture is now established.

---

# Next Document

The next Network Design document is:

`05-VLAN-Design.md`

The VLAN Design will translate the approved logical segmentation into Layer 2 network identifiers.

It will determine:

- Which implemented networks require VLANs
- VLAN IDs
- VLAN names
- VLAN-to-subnet mappings
- Tagged and untagged traffic requirements
- pfSense VLAN interfaces
- VMware VLAN considerations
- Future reserved VLAN assignments

VLAN configuration will remain documented rather than deployed until the VMware and pfSense implementation phases.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
