# Stoneleaf Services — Technical Requirements

**No Stone Left Unturned**

## Purpose

This document defines the technical requirements for the Stoneleaf Services environment.

These requirements translate the organizational and business requirements defined in `Business-Requirements.md` into infrastructure, networking, identity, security, virtualization, operating system, logging, monitoring, investigation, and cloud capabilities.

This document defines what the technical environment must support.

Specific architecture and implementation decisions, including IP addressing, subnet design, VLAN configuration, Active Directory namespace, firewall rules, virtual machine resource allocation, and detailed installation procedures, will be defined in later design and implementation documentation.

---

## Technical Environment Overview

Stoneleaf Services will initially operate as a virtualized on-premises environment designed to simulate the infrastructure of a 40-person professional services organization.

The environment must support:

- 40 unique fictional employee identities
- Multiple organizational departments
- Role-based access requirements
- Windows and Linux systems
- Centralized identity management
- Network infrastructure
- Security controls
- Logging and monitoring
- Troubleshooting exercises
- Digital investigation exercises
- Intelligence and analytical activities
- Future cloud and hybrid infrastructure

The initial permanent virtual infrastructure will include:

| Hostname | Platform | Primary Role |
| --- | --- | --- |
| `SLS-FW01` | pfSense | Firewall, router, DHCP, NAT |
| `SLS-DC01` | Windows Server | Active Directory Domain Services and DNS |
| `SLS-LNX01` | Ubuntu Server 24.04 LTS | Linux server administration and services |
| `SLS-WS01` | Windows 11 | Investigations workstation |
| `SLS-WS02` | Windows 11 | Intelligence and analysis workstation |
| `SLS-WS03` | Windows 11 | Management and administrative workstation |

VMware will provide the initial virtualization platform.

Future development will extend the environment into Microsoft Azure and Microsoft Entra ID.

---

# Virtualization Requirements

## TR-01 — Virtualization Platform

Stoneleaf Services requires a virtualization platform capable of hosting the planned on-premises infrastructure.

The virtualization platform must support:

- Multiple virtual machines
- Virtual CPU allocation
- Virtual memory allocation
- Virtual disk allocation
- Virtual network adapters
- Multiple virtual networks
- Isolated virtual networking
- External network connectivity
- Virtual machine snapshots where appropriate
- Virtual machine cloning where appropriate
- Virtual machine import and export where supported
- Virtual machine recovery
- Windows Server guests
- Windows 11 guests
- Linux guests
- pfSense

Virtual machines must be configured according to documented Stoneleaf Services standards.

---

## TR-02 — Virtual Machine Naming

Every permanent Stoneleaf Services virtual machine must have a unique standardized hostname.

The initial naming convention will use the prefix:

`SLS-`

Initial systems include:

- `SLS-FW01`
- `SLS-DC01`
- `SLS-LNX01`
- `SLS-WS01`
- `SLS-WS02`
- `SLS-WS03`

Detailed naming conventions will be maintained in `Naming-Standards.md`.

---

# Network Requirements

## TR-03 — Private Internal Network

Stoneleaf Services requires a private internal IPv4 network capable of supporting the simulated organization.

The network must support:

- Static addressing
- Dynamic addressing
- Internal communication
- Internet connectivity
- Internal DNS
- Active Directory
- Routing
- Firewalling
- NAT
- Troubleshooting
- Future segmentation
- Future cloud connectivity
- Future hybrid connectivity

The exact network topology and addressing architecture will be defined during network design.

---

## TR-04 — Network Segmentation Capability

The network architecture must support future logical segmentation without requiring complete redesign.

Potential future network categories may include:

- Infrastructure
- Servers
- User endpoints
- Management
- Security
- Investigation systems
- Testing systems
- Guest systems
- Cloud-connected resources

The requirement to support segmentation does not require all potential network segments to be implemented during the initial deployment.

Segmentation decisions will be based on security, operational, training, and infrastructure requirements identified during network design.

---

## TR-05 — Edge Firewall and Router

Stoneleaf Services requires a dedicated firewall and routing platform.

`SLS-FW01` will use pfSense.

The firewall/router must support:

- WAN connectivity
- LAN connectivity
- IPv4 routing
- Stateful firewalling
- DHCP
- Network Address Translation
- Traffic logging
- Firewall-rule management
- VPN capabilities
- Future network segmentation
- Future inter-network routing
- Future hybrid connectivity

---

## TR-06 — Network Interfaces

`SLS-FW01` must contain sufficient virtual network interfaces to separate internal and external network connectivity.

The initial configuration must support at minimum:

- External/WAN connectivity
- Internal/LAN connectivity

Additional interfaces or logical networks may be introduced when required by future network designs.

---

## TR-07 — DHCP

Stoneleaf Services requires centralized dynamic network configuration for appropriate endpoint systems.

The initial DHCP service will be provided by pfSense.

DHCP must be capable of providing clients with required configuration including:

- IPv4 address
- Subnet mask
- Default gateway
- DNS server information
- Other required DHCP options

Infrastructure systems requiring predictable addressing must use documented controlled addressing.

The exact DHCP scope and exclusions will be determined during network design.

---

## TR-08 — Routing

Stoneleaf Services requires routing between authorized networks.

The routing architecture must support:

- Internal network communication
- Internal-to-external communication
- Return traffic
- Future additional internal networks
- Future VPN connectivity
- Future Azure connectivity

Routing decisions must be documented as the network architecture develops.

---

## TR-09 — Network Address Translation

Stoneleaf Services requires Network Address Translation for appropriate communication between private internal networks and external networks.

pfSense will provide initial NAT functionality.

NAT must permit authorized systems to access external resources while maintaining private internal addressing.

---

## TR-10 — Network Firewalling

Stoneleaf Services requires stateful network firewall controls.

Firewall capabilities must support:

- Source-based rules
- Destination-based rules
- Protocol-based rules
- Port-based rules
- Traffic logging
- Rule validation
- Controlled inbound communication
- Controlled outbound communication
- Future inter-network filtering

Firewall configuration must follow least-privilege principles where practical.

---

# Identity and Directory Requirements

## TR-11 — Active Directory Domain Services

Stoneleaf Services requires centralized Windows identity and directory management.

Windows Server Active Directory Domain Services must support:

- 40 unique simulated employee identities
- Computer accounts
- Organizational Units
- Security groups
- Group Policy
- Authentication
- Authorization
- Administrative delegation
- Role-based access
- Employee onboarding
- Employee role changes
- Employee offboarding

The Active Directory architecture must be documented before full user deployment.

---

## TR-12 — Active Directory Namespace

Stoneleaf Services requires a documented Active Directory domain namespace.

The namespace must:

- Support the Stoneleaf Services identity environment
- Support internal DNS
- Support domain-joined systems
- Support future expansion
- Avoid unnecessary naming conflicts
- Support future cloud and hybrid identity requirements

The actual domain name will be selected during directory and network design.

---

## TR-13 — Unique Employee Identities

Each of the 40 simulated employees must receive a unique fictional organizational identity.

Each identity must eventually include documented attributes such as:

- First name
- Last name
- Employee ID
- Job title
- Department
- Manager
- Username
- User Principal Name
- Organizational email address
- Active Directory account
- Organizational Unit
- Security-group memberships
- Access requirements
- Privilege level
- Workstation assignment where applicable
- Cloud identity where applicable

All employee identities will be synthetic and created exclusively for the Stoneleaf Services environment.

Generic numbered accounts will not serve as the primary identities of simulated employees.

---

## TR-14 — Organizational Units

Active Directory must contain a documented Organizational Unit structure.

The OU architecture must support:

- Users
- Workstations
- Servers
- Administrative accounts
- Group Policy application
- Administrative delegation
- Appropriate organizational separation

OU design must be based primarily on administrative and policy requirements rather than simply duplicating the organizational chart.

---

## TR-15 — Security Groups

Stoneleaf Services must use security groups to manage access wherever practical.

Security groups must support:

- Departmental access
- Functional access
- Resource access
- Management access
- Investigation access
- Intelligence access
- IT access
- Security access
- Administrative roles

Direct assignment of permissions to individual users should be minimized when group-based permissions are practical.

---

## TR-16 — Privileged Accounts

Administrative access must be separated from normal user activity where practical.

Personnel requiring elevated access should use separate privileged identities for administrative activities.

Privileged accounts must be:

- Individually identifiable
- Documented
- Restricted
- Assigned only when required
- Monitored where appropriate

---

## TR-17 — Employee Lifecycle Support

The identity architecture must support:

### Onboarding

- Identity creation
- Account provisioning
- Group assignment
- Resource access
- Workstation access

### Role Changes

- Department transfers
- Promotions
- Management changes
- Group modifications
- Permission changes

### Offboarding

- Account disablement
- Access revocation
- Group removal
- Administrative review
- Appropriate record preservation

---

# DNS Requirements

## TR-18 — Internal DNS

Stoneleaf Services requires centralized internal DNS.

Windows Server DNS on `SLS-DC01` will provide the initial internal DNS service.

Internal DNS must support:

- Active Directory
- Domain controllers
- Domain-joined systems
- Internal hostname resolution
- Required service records
- Internal infrastructure

Domain-joined systems must use the appropriate Stoneleaf Services internal DNS service for Active Directory-related name resolution.

---

## TR-19 — External DNS Resolution

Internal systems must be capable of resolving authorized external domain names.

The DNS architecture must provide a documented method for external name resolution.

The exact forwarding or recursive-resolution design will be established during DNS design and implementation.

---

# Windows Server Requirements

## TR-20 — Windows Server Infrastructure

Stoneleaf Services requires Windows Server infrastructure capable of providing centralized identity and administrative services.

`SLS-DC01` must initially support:

- Active Directory Domain Services
- DNS
- Group Policy
- Authentication
- Authorization
- Identity management
- Security logging
- Administrative tools

The domain controller must use predictable network configuration.

---

## TR-21 — Group Policy

Stoneleaf Services requires centralized policy management for domain-joined Windows systems.

Group Policy must support configuration of areas such as:

- Account policies
- Security settings
- User configuration
- Computer configuration
- Administrative restrictions
- Windows security
- Logging
- Workstation configuration

Policies must be documented and validated.

---

# Windows Endpoint Requirements

## TR-22 — Windows Workstations

Stoneleaf Services requires Windows workstations representing different organizational functions.

The initial environment will include:

- `SLS-WS01`
- `SLS-WS02`
- `SLS-WS03`

Workstations must support:

- Network connectivity
- DHCP where appropriate
- Internal DNS
- Domain membership
- Domain authentication
- Group Policy
- Role-based access
- Security controls
- System logging
- Security logging
- Troubleshooting exercises

---

## TR-23 — Workstation Functional Roles

The initial workstations will represent different organizational functions.

### SLS-WS01

**Primary Function:** Investigations

### SLS-WS02

**Primary Function:** Intelligence and Analysis

### SLS-WS03

**Primary Function:** Management and Administration

These distinctions must support future role-based access, security, investigation, and analytical exercises.

---

# Linux Requirements

## TR-24 — Linux Server

Stoneleaf Services requires Linux server capability.

`SLS-LNX01` will initially use Ubuntu Server 24.04 LTS.

The Linux environment must support practical experience with:

- Command-line administration
- TCP/IP
- DNS
- SSH
- Users
- Groups
- File ownership
- Permissions
- Package management
- Processes
- Services
- Storage
- Logging
- Firewall configuration
- Security hardening
- Scripting
- Automation
- Troubleshooting

---

## TR-25 — Secure Remote Administration

`SLS-LNX01` must support secure remote administration.

SSH will provide the initial remote administrative method.

Remote administration must support appropriate authentication, authorization, logging, and security controls.

---

# Security Requirements

## TR-26 — Least Privilege

Stoneleaf Services systems must follow least-privilege principles.

Users must receive only the access required for their assigned organizational responsibilities.

Administrative privileges must be restricted and documented.

---

## TR-27 — Authentication Security

The environment must support configurable authentication controls.

Capabilities must include or eventually support:

- Password policies
- Account lockout policies
- Privileged-account controls
- Authentication logging
- Failed-authentication monitoring
- Administrative-account separation
- Multifactor authentication where supported

---

## TR-28 — System Hardening

Stoneleaf Services systems must support documented security-hardening procedures.

Hardening may include:

- Disabling unnecessary services
- Host firewall configuration
- Secure account configuration
- Patch management
- Least privilege
- Logging configuration
- Secure remote administration
- Reduction of unnecessary network exposure

Hardening procedures must be validated to ensure required functionality remains operational.

---

## TR-29 — Patch and Update Management

Stoneleaf Services systems must be capable of receiving security and software updates.

Update requirements apply to:

- Windows Server
- Windows workstations
- Ubuntu Server
- pfSense
- VMware
- Security tools
- Future cloud systems

Update failures must be identifiable and capable of being troubleshot.

---

# Logging and Monitoring Requirements

## TR-30 — System Logging

Stoneleaf Services systems must generate sufficient logging to support:

- Administration
- Troubleshooting
- Security monitoring
- Incident response
- Digital investigations

Relevant log sources will eventually include:

- pfSense
- Windows Server
- Active Directory
- DNS
- Windows endpoints
- Ubuntu Server
- Authentication systems
- Security tools
- Azure resources

---

## TR-31 — Centralized Logging

The architecture must support future centralized collection and analysis of logs from multiple systems.

Centralized logging must eventually allow events from different systems to be correlated during:

- Troubleshooting
- Security monitoring
- Incident response
- Digital investigations

The specific centralized logging platform will be selected during a later design phase.

---

## TR-32 — Security Monitoring

The environment must support future security-monitoring capabilities.

Monitoring should eventually provide visibility into:

- Authentication activity
- Administrative activity
- Endpoint events
- Network activity
- Firewall activity
- Security alerts
- Suspicious behavior
- Cloud activity

---

# Troubleshooting Requirements

## TR-33 — Controlled Troubleshooting Environment

The Stoneleaf Services environment must allow controlled technical failures to be introduced, identified, diagnosed, corrected, and documented.

Troubleshooting scenarios must be capable of involving:

- IP addressing
- Subnet configuration
- DHCP
- DNS
- Default gateways
- Routing
- NAT
- Firewall rules
- Active Directory
- Authentication
- Authorization
- Group Policy
- Windows services
- Linux services
- Permissions
- Logging
- Cloud connectivity
- Security controls

---

## TR-34 — Troubleshooting Tools

The environment must support standard administrative and troubleshooting utilities.

### Windows

Examples include:

- `ipconfig`
- `ping`
- `tracert`
- `nslookup`
- `netstat`
- `route`
- `arp`
- PowerShell
- Event Viewer

### Linux

Examples include:

- `ip`
- `ping`
- `traceroute`
- `dig`
- `nslookup`
- `ss`
- `journalctl`
- `systemctl`
- `curl`
- `ssh`

### Network Analysis

Future capabilities may include:

- Wireshark
- Packet capture
- pfSense diagnostics
- Centralized log analysis

---

## TR-35 — Troubleshooting Documentation

Troubleshooting exercises must be documented using a consistent methodology.

Documentation should include:

1. Problem statement
2. Symptoms
3. Scope
4. Relevant architecture
5. Evidence collected
6. Hypotheses
7. Tests performed
8. Results
9. Root cause
10. Corrective action
11. Validation
12. Lessons learned

---

# Investigation Requirements

## TR-36 — Digital Investigation Capability

The environment must support future simulated digital investigations.

Investigation exercises may use:

- Windows event logs
- Linux logs
- Firewall logs
- DNS information
- Authentication records
- File-system artifacts
- File metadata
- Network traffic
- Endpoint artifacts
- Security alerts

Investigation activities must use authorized lab systems and appropriate simulated, generated, or sanitized data.

---

## TR-37 — Evidence Handling

Future investigation exercises must support documented evidence-handling procedures.

Where applicable, investigation documentation should identify:

- Evidence source
- Collection method
- Date and time
- Integrity considerations
- Storage location
- Analysis performed
- Findings

More formal digital-forensics procedures may be introduced as Stoneleaf Services develops those capabilities.

---

# Intelligence and Analysis Requirements

## TR-38 — Intelligence and Analysis Capability

The environment must support future intelligence collection and analytical exercises.

`SLS-WS02` will initially provide the primary simulated intelligence and analysis workstation.

Capabilities may include:

- Open-source research
- Information collection
- Source evaluation
- Information verification
- Data organization
- Timeline analysis
- Link analysis
- Analytical writing
- Reporting

Specific analytical tools will be selected when supported by documented requirements.

---

## TR-39 — Investigation Workstation Capability

`SLS-WS01` will initially provide the primary simulated investigation workstation.

Capabilities may include:

- Digital investigations
- Log review
- Evidence review
- Timeline development
- Incident investigation
- Digital-forensics exercises
- Investigation documentation

Specialized tools will be introduced as requirements and training objectives develop.

---

# Backup and Recovery Requirements

## TR-40 — Documentation Backup

Stoneleaf Services technical documentation must be protected against accidental loss.

Documentation may be maintained across:

- GitHub
- Local storage
- Cloud storage
- Backup storage

Sensitive information must not be published to public repositories.

---

## TR-41 — Configuration Backup

Critical infrastructure configurations must eventually be backed up.

Examples may include:

- pfSense configuration
- Network configuration
- Active Directory-related configuration and documentation
- Linux configuration
- Scripts
- Security configurations
- Cloud configurations where appropriate

Backup procedures must be documented.

---

## TR-42 — Virtual Machine Recovery

The virtualization architecture must support recovery of important virtual machines.

Recovery methods may include:

- Rebuilding from documented procedures
- Restoring backups
- Restoring configuration data
- Recreating virtual machines
- Using snapshots where appropriate

Snapshots must not be treated as a replacement for proper backups.

---

# Cloud and Hybrid Requirements

## TR-43 — Microsoft Azure

The architecture must support future Microsoft Azure integration.

Future Azure capabilities may include:

- Virtual networks
- Subnets
- Virtual machines
- Storage
- Network security controls
- Monitoring
- Logging
- Identity integration
- Security services

Cloud resources must be designed with security and cost control in mind.

---

## TR-44 — Microsoft Entra ID

Stoneleaf Services requires future Microsoft Entra ID capability.

Future Entra ID development may include:

- Cloud identities
- Groups
- Role-Based Access Control
- Multifactor authentication
- Identity security
- Administrative roles
- Access management
- Cloud authentication

The relationship between on-premises Active Directory and Microsoft Entra ID will be defined during hybrid identity design.

---

## TR-45 — Hybrid Connectivity

The architecture must support future secure connectivity between the Stoneleaf Services on-premises environment and appropriate cloud resources.

Potential technologies may include:

- Site-to-site VPN
- Azure VPN services
- pfSense VPN capabilities
- Azure virtual networking

The specific architecture will be determined during cloud and hybrid network design.

---

# Documentation Requirements

## TR-46 — Implementation Runbooks

Major infrastructure components must have detailed implementation runbooks.

Runbooks should include:

- Purpose
- Prerequisites
- Dependencies
- Required software
- Virtual machine specifications
- Installation procedures
- Configuration procedures
- Verification procedures
- Expected results
- Troubleshooting guidance
- Rollback or recovery procedures
- Screenshots where useful
- Lessons learned

Runbooks should contain sufficient detail to reproduce the intended configuration.

---

## TR-47 — Architecture Documentation

Stoneleaf Services must maintain current architecture documentation.

Documentation should eventually include:

- Logical network diagrams
- Physical host information
- Virtual infrastructure
- Network addressing
- Routing
- DNS
- DHCP
- Firewall architecture
- Active Directory
- Cloud infrastructure
- Security architecture
- Logging architecture

---

## TR-48 — Change Documentation

Significant infrastructure and configuration changes must be documented according to the Stoneleaf Services change-management process.

Documentation must distinguish between:

- Planned configuration
- Implemented configuration
- Validation results
- Unexpected results
- Corrective actions

---

# Resource Requirements

## TR-49 — Storage

The Stoneleaf Services host must provide sufficient storage for:

- Virtual machine operating systems
- Virtual disks
- Software
- Logs
- Lab data
- Investigation exercises
- Temporary snapshots
- Security tools

Storage utilization must be monitored to prevent exhaustion of host storage.

Full infrastructure deployment may be deferred until sufficient SSD capacity is available.

---

## TR-50 — Memory

Virtual machine memory allocations must account for available host RAM.

Memory must be allocated according to workload requirements rather than unnecessarily maximizing RAM for individual virtual machines.

Not all virtual machines are required to operate simultaneously.

---

## TR-51 — Processing Resources

Virtual CPU allocation must account for available host processor resources.

Virtual machines must receive sufficient processing capability for their intended workloads without unnecessary resource allocation.

---

## TR-52 — External Storage

The architecture must support future external storage for purposes including:

- Backups
- Archived virtual machines
- Installation media
- Lab datasets
- Investigation datasets
- Configuration archives

External storage architecture will be documented when implemented.

---

# Scalability Requirements

## TR-53 — Infrastructure Expansion

The architecture must allow additional infrastructure to be introduced without requiring complete redesign.

Future systems may include:

- Additional Windows servers
- Additional Linux servers
- Additional endpoints
- Logging servers
- Monitoring systems
- Security platforms
- Investigation systems
- Analytical systems
- Temporary testing systems
- Cloud systems

Permanent systems must have a documented purpose.

---

## TR-54 — Organizational Expansion

The technical architecture must support changes to the simulated organization.

The environment must permit:

- Additional users
- New departments
- Department restructuring
- Management changes
- New security groups
- New access requirements
- Additional workstations
- Additional administrative roles

The initial 40-person organization establishes the baseline rather than a permanent technical maximum.

---

# Validation Requirements

## TR-55 — Network Validation

The completed initial network must demonstrate that:

- Endpoints receive appropriate network configuration.
- Static systems retain intended addresses.
- Internal systems communicate as authorized.
- Default gateways are reachable.
- Internet connectivity functions.
- Internal DNS functions.
- External DNS resolution functions.
- NAT functions.
- Firewall rules operate as intended.

---

## TR-56 — Active Directory Validation

The completed directory environment must demonstrate that:

- The Active Directory domain is operational.
- DNS supports Active Directory.
- Windows workstations can join the domain.
- Domain users can authenticate.
- Security groups function.
- Group Policy can be applied.
- Administrative access can be controlled.
- Authentication events are logged.
- Individual employee identities function according to assigned roles.

---

## TR-57 — Linux Validation

The completed Linux environment must demonstrate that:

- `SLS-LNX01` has appropriate network connectivity.
- DNS resolution functions.
- SSH administration functions.
- User and group management functions.
- Services can be administered.
- Logs can be reviewed.
- Security controls can be applied.
- Linux failures can be systematically troubleshot.

---

## TR-58 — Security Validation

The environment must provide methods for validating implemented security controls.

Validation may include:

- Access-control testing
- Firewall-rule testing
- Authentication testing
- Group-membership testing
- Permission testing
- Log verification
- Security-event generation
- Configuration review

---

## TR-59 — Documentation Validation

Major implementation procedures must be validated against the actual environment.

If documented procedures do not reproduce the intended configuration or result, the documentation must be corrected.

Documentation must reflect the implemented environment rather than outdated planned configurations.

---

# Current Technical Baseline

| Component | Planned Technology |
| --- | --- |
| Virtualization | VMware |
| Firewall / Router | pfSense |
| DHCP | pfSense |
| NAT | pfSense |
| Directory Services | Windows Server Active Directory Domain Services |
| Internal DNS | Windows Server DNS |
| Linux | Ubuntu Server 24.04 LTS |
| Endpoints | Windows 11 |
| Cloud | Microsoft Azure |
| Cloud Identity | Microsoft Entra ID |
| Version Control / Portfolio | GitHub |
| Detailed Runbooks | Microsoft Word |

This baseline may be revised through documented design decisions and change management.

---

# Requirements Traceability

Technical requirements should remain traceable to organizational and business requirements.

| Business Need | Technical Requirement |
| --- | --- |
| 40 individual employees | 40 unique fictional identities supported through centralized identity management |
| Centralized identity | Windows Server Active Directory Domain Services |
| Role-based access | Security groups and documented permissions |
| Employee lifecycle | Account provisioning, modification, disablement, and access revocation |
| Automatic endpoint configuration | Centralized DHCP |
| Internal name resolution | Windows Server DNS |
| Internet connectivity | Routing and NAT |
| Network security | Stateful firewall |
| Windows administration | Active Directory and Group Policy |
| Linux capability | Ubuntu Server |
| Troubleshooting | Multi-system environment supporting controlled failures |
| Security investigations | System, authentication, endpoint, DNS, and firewall logging |
| Intelligence analysis | Dedicated analytical workstation capability |
| Cloud expansion | Microsoft Azure and Entra ID |
| Reproducibility | Architecture documentation and implementation runbooks |
| Scalability | Expandable network, identity, virtualization, and cloud architecture |

---

# Current Status

**Phase:** Foundation Planning and Documentation

**Implementation Status:** Full infrastructure deployment is deferred pending sufficient local storage capacity.

The technical requirements established in this document will guide subsequent architecture, design, implementation, testing, and validation.

Technical requirements may be revised through the Stoneleaf Services change-management process as organizational needs and technical capabilities develop.

---

# Next Foundation Document

The next Foundation document is:

**`Hardware-Inventory.md`**

The Hardware Inventory will document the physical systems, storage devices, networking equipment, peripherals, and other hardware currently available to Stoneleaf Services.

The inventory will provide the factual hardware baseline used later to determine virtual machine resource allocations, storage architecture, backup capacity, and infrastructure upgrade requirements.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
