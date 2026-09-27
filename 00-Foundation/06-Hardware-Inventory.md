# Stoneleaf Services — Hardware Inventory

**No Stone Left Unturned**

## Purpose

This document maintains the physical hardware inventory for the Stoneleaf Services technical environment.

The inventory establishes the hardware resources currently available to support:

- Virtualization
- Networking
- Systems administration
- Cybersecurity
- Digital investigations
- Intelligence and analysis
- Data storage
- Backup and recovery
- Technical training
- Stoneleaf Services project development

This document distinguishes between currently available hardware and planned infrastructure upgrades.

Hardware should be added, removed, or updated as the Stoneleaf Services environment develops.

---

# Inventory Status Definitions

The following status values will be used throughout this document:

| Status | Definition |
| --- | --- |
| Active | Currently available and actively used |
| Available | Owned and available but not currently assigned |
| Planned | Intended future acquisition or upgrade |
| Retired | No longer used |
| Unknown | Specification or status requires verification |

---

# HW-001 — Primary Virtualization Host

## System Information

| Attribute | Specification |
| --- | --- |
| Asset ID | `HW-001` |
| Device | HP OMEN 17 |
| Model | 17-cm2xxx Series |
| Device Type | Laptop / Primary Lab Host |
| Processor | Intel Core i7-13700HX |
| Memory | 64 GB RAM |
| Primary Function | VMware virtualization and Stoneleaf Services lab |
| Status | Active |

## Intended Roles

`HW-001` serves as the primary computing platform for the Stoneleaf Services home lab.

Primary uses include:

- VMware virtualization
- Windows Server virtual machines
- Windows workstation virtual machines
- Linux virtual machines
- pfSense
- Networking exercises
- Cybersecurity exercises
- Troubleshooting labs
- Digital investigation exercises
- Intelligence and analysis tools
- Future hybrid-cloud administration

---

## Memory

The system currently contains:

**64 GB RAM**

Available memory will be shared between:

- Host operating system
- VMware
- Infrastructure virtual machines
- Workstation virtual machines
- Security tools
- Investigation tools
- Other applications

Virtual machine memory allocations will be determined during VMware design.

Resource allocation should preserve sufficient memory for the host operating system while providing adequate resources to required virtual machines.

---

## Internal Storage

### Current Storage

| Device | Capacity | Interface | Function | Status |
| --- | ---: | --- | --- | --- |
| Internal SSD 1 | 512 GB | NVMe M.2 | Operating system / current storage | Active |

The existing internal SSD currently limits the amount of virtual infrastructure that can be deployed simultaneously.

Full Stoneleaf Services virtual infrastructure deployment will therefore remain limited until additional internal SSD capacity is installed.

---

## Internal Storage Expansion

The primary virtualization host contains multiple NVMe storage capabilities.

The planned storage strategy is to increase internal SSD capacity to provide sufficient space for:

- Virtual machines
- Virtual disks
- Operating system images
- Software
- Logs
- Security datasets
- Investigation datasets
- Temporary snapshots
- Lab projects

### Planned Upgrade

| Component | Target | Status |
| --- | --- | --- |
| Additional internal NVMe SSD | Up to 4 TB | Planned |
| Existing SSD relocation if required | Secondary M.2 slot | Planned |

Final SSD selection and installation configuration will be documented when the upgrade is performed.

---

# HW-002 — External SSD

| Attribute | Specification |
| --- | --- |
| Asset ID | `HW-002` |
| Device Type | External solid-state storage |
| Capacity | 1 TB |
| Interface | USB |
| Primary Function | Portable / supplemental storage |
| Status | Active |

# Potential Stoneleaf Services uses include:

- Installation media
- ISO storage
- Temporary lab files
- Software installers
- Data transfer
- Selected lab datasets
- Temporary VM storage where appropriate

This device should not automatically be considered a primary backup solution.

---

# Storage Summary

## Current Local Storage

| Asset | Capacity | Type | Status |
| --- | ---: | --- | --- |
| `HW-001` Internal SSD | 512 GB | NVMe SSD | Active |
| `HW-002` External Storage | 1 TB | External SSD | Active |

Storage physically installed in separate computers should not be treated as a single shared storage pool unless a future architecture specifically provides network-accessible storage.

---

# Planned Storage Expansion

Stoneleaf Services requires additional storage as the lab expands.

Potential future storage requirements include:

- Larger internal NVMe storage
- Virtual machine storage
- Backup storage
- Redundant storage
- Investigation storage
- Archived virtual machines
- ISO and installation-media storage
- Log retention
- Configuration backups
- Project archives

A future dedicated storage system or server may be considered as requirements develop.

Potential future technologies may include:

- Direct-attached storage
- Network-attached storage
- RAID
- Large-capacity hard drives
- SSD storage
- Backup drives

No final dedicated storage architecture has been selected.

---

# Future Storage Server / NAS

Stoneleaf Services may eventually deploy dedicated network storage.

A future storage platform could support:

- Centralized file storage
- Virtual machine backups
- Configuration backups
- Documentation backups
- Investigation datasets
- ISO storage
- Archived projects
- Log archives
- Recovery data

A future storage design may incorporate multiple high-capacity drives and RAID or another redundancy technology.

RAID will not be considered a replacement for independent backups.

The storage architecture will be documented separately before implementation.

---

# Network Hardware

The initial Stoneleaf Services lab primarily uses virtual networking provided through VMware and pfSense.

## Current Network Infrastructure

| Component | Function | Status |
| --- | --- | --- |
| Existing home network | External network / internet connectivity | Active |
| VMware virtual networking | Lab virtual networking | Planned / In Development |
| `SLS-FW01` | Virtual firewall/router | Planned |

Specific physical networking hardware will be added to this inventory after model information and technical specifications are verified.

Potential future additions may include:

- Managed switch
- VLAN-capable switch
- Dedicated wireless access point
- Network adapters
- USB Ethernet adapters
- Additional Ethernet interfaces
- Dedicated lab networking equipment

---

# Removable Media

Removable media may eventually be maintained for:

- Operating system installation
- Bootable utilities
- Recovery tools
- Digital-forensics tools
- Evidence-handling exercises
- Secure data transfer
- Firmware updates

Individual removable-media devices should receive asset identifiers if they become part of the permanent Stoneleaf Services equipment inventory.

---

# Cloud Storage

Cloud storage is not physical hardware and therefore is not counted as local hardware capacity.

Stoneleaf Services currently has access to cloud storage that may supplement the physical environment.

Cloud storage should be documented separately in the software, service, or cloud inventory as appropriate.

Cloud storage does not eliminate the requirement for an appropriate local and independent backup strategy.

---

# Hardware Resource Considerations

## Virtualization

The primary virtualization host must provide sufficient:

- CPU resources
- Memory
- Storage capacity
- Storage performance
- Network connectivity

for the Stoneleaf Services virtual environment.

The primary current infrastructure constraint is local SSD capacity.

---

## Cybersecurity

Future cybersecurity workloads may increase requirements for:

- Memory
- CPU
- Storage
- Log retention
- Network interfaces
- Dedicated test systems

Resource requirements should be evaluated before additional permanent systems are deployed.

---

## Digital Investigations

Digital investigation and forensic workloads can require substantial storage.

Future planning should account for:

- Disk images
- Memory captures
- Network captures
- Log collections
- Extracted artifacts
- Investigation working copies
- Evidence copies
- Analysis output

Investigation datasets should not automatically share storage with critical infrastructure backups.

---

## Logging

Centralized logging may produce significant long-term storage requirements.

Future logging architecture should account for:

- Daily ingestion volume
- Retention period
- Search performance
- Archive requirements
- Available storage
- Cloud costs where applicable

---

# Hardware Identification Standard

Permanent Stoneleaf Services hardware should receive a unique asset identifier.

The initial format is:

`HW-###`

Examples:

- `HW-001`
- `HW-002`
- `HW-003`

Asset identifiers remain associated with the physical device even if its operational role later changes.

---

# Future Asset Records

As the environment develops, hardware inventory records should include where applicable:

- Asset ID
- Manufacturer
- Model
- Serial number
- Device type
- Processor
- Memory
- Storage
- Network interfaces
- Operating system
- Assigned role
- Acquisition date
- Warranty information
- Status
- Notes

Sensitive identifiers such as serial numbers should not be published in the public GitHub repository.

Detailed private inventory records may contain information intentionally omitted from public documentation.

---

# Inventory Security

Public Stoneleaf Services documentation must not expose unnecessary information that could create security or privacy risks.

The public repository should exclude:

- Device serial numbers
- MAC addresses unless sanitized
- Public IP addresses
- Private credentials
- Authentication information
- Encryption keys
- Recovery keys
- Personally identifiable information
- Sensitive network information

Private documentation may contain additional operational details where appropriate.

---

# Planned Hardware Categories

As Stoneleaf Services develops, additional hardware may be acquired in categories including:

### Compute

- Additional virtualization hardware
- Dedicated server hardware
- Administrative workstations
- Investigation workstations

### Storage

- High-capacity HDDs
- SSDs
- External backup drives
- NAS or storage server hardware
- Redundant storage

### Networking

- Managed switches
- Network adapters
- Cabling
- Wireless infrastructure
- Dedicated lab networking equipment

### Backup

- Independent backup drives
- Redundant storage
- Offline backup media

Hardware should be acquired based on documented requirements rather than adding equipment without a defined purpose.

---

# Current Hardware Constraints

The primary known constraint affecting the Stoneleaf Services lab is storage capacity on the primary virtualization host.

The current 512 GB internal SSD limits the practical number and size of virtual machines that can be maintained.

The planned internal storage expansion will significantly increase the capacity available for:

- Windows Server
- Windows workstations
- Linux systems
- pfSense
- Snapshots
- Screenshots
- Security tools
- Investigation tools
- Lab datasets

Until the storage expansion is completed, documentation and infrastructure planning remain the primary focus.

---

# Current Status

**Inventory Status:** Initial Baseline

**Primary Virtualization Host:** `HW-001`

**Primary Constraint:** Internal SSD capacity

**Current Priority:** Complete infrastructure documentation and expand primary-host storage before full virtual machine deployment.

This inventory will be updated as hardware is acquired, upgraded, reassigned, or retired.

---

# Next Foundation Document

The next Foundation document is:

**`Software-Inventory.md`**

The Software Inventory will document the software platforms, operating systems, virtualization software, administrative tools, security tools, cloud services, and other software used or planned for the Stoneleaf Services environment.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
