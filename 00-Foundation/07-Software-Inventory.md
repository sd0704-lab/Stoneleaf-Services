# Stoneleaf Services — Software Inventory

**No Stone Left Unturned**

## Purpose

This document maintains the software, operating system, virtualization, cloud, administrative, security, investigation, and analytical technology inventory for the Stoneleaf Services environment.

The inventory establishes the software baseline used to support:

- Information technology
- Networking
- Systems administration
- Virtualization
- Cybersecurity
- Troubleshooting
- Digital investigations
- Intelligence collection
- Intelligence analysis
- Cloud administration
- Documentation
- Stoneleaf Services project development

This document distinguishes between software currently used, software selected for planned deployment, and technologies reserved for future evaluation.

Specific software should be added when supported by a documented technical, operational, training, or project requirement.

---

# Inventory Status Definitions

| Status | Definition |
| --- | --- |
| Active | Currently installed and actively used |
| Available | Available for use but not currently deployed |
| Planned | Selected for future deployment |
| Evaluation | Being considered but not selected |
| Retired | No longer used |
| Unknown | Installation, version, or licensing status requires verification |

---

# Software Identification Standard

Permanent software platforms documented by Stoneleaf Services should receive a unique software identifier.

The initial format is:

`SW-###`

Examples:

- `SW-001`
- `SW-002`
- `SW-003`

Software identifiers allow applications and platforms to be referenced consistently across:

- Technical documentation
- Build procedures
- Troubleshooting reports
- Change records
- Security documentation
- Incident reports
- Investigation documentation

---

# Core Software Inventory

## SW-001 — VMware

| Attribute | Information |
| --- | --- |
| Software ID | `SW-001` |
| Category | Virtualization |
| Product | VMware |
| Function | Virtual machine hosting and virtual networking |
| Status | Active / Planned for Stoneleaf Lab |

### Stoneleaf Services Use

VMware will provide the primary virtualization platform for the initial Stoneleaf Services environment.

VMware will support:

- pfSense
- Windows Server
- Windows 11
- Ubuntu Server
- Virtual networking
- Isolated lab networks
- Virtual network adapters
- VM resource allocation
- Snapshots where appropriate
- Troubleshooting exercises

Exact VMware edition and version information should be recorded after the production lab configuration is finalized.

---

## SW-002 — pfSense

| Attribute | Information |
| --- | --- |
| Software ID | `SW-002` |
| Category | Networking / Security |
| Product | pfSense |
| Planned Hostname | `SLS-FW01` |
| Function | Firewall, router, DHCP, NAT |
| Status | Planned |

### Planned Functions

pfSense will initially provide:

- Firewalling
- Routing
- DHCP
- NAT
- Network logging
- Traffic control
- Network diagnostics

Future functionality may include:

- VPN services
- Additional network interfaces
- Network segmentation
- Inter-network routing
- Additional firewall policies
- Hybrid-cloud connectivity

---

## SW-003 — Microsoft Windows Server

| Attribute | Information |
| --- | --- |
| Software ID | `SW-003` |
| Category | Server Operating System |
| Product | Microsoft Windows Server |
| Planned Hostname | `SLS-DC01` |
| Function | Centralized Windows infrastructure |
| Status | Planned |

### Planned Roles

Windows Server will initially support:

- Active Directory Domain Services
- DNS
- Group Policy
- Authentication
- Authorization
- User management
- Computer management
- Security groups
- Organizational Units
- Security logging
- Administrative tools

The exact Windows Server edition and version will be documented before deployment.

---

## SW-004 — Active Directory Domain Services

| Attribute | Information |
| --- | --- |
| Software ID | `SW-004` |
| Category | Identity and Directory Services |
| Product | Active Directory Domain Services |
| Host | `SLS-DC01` |
| Function | Centralized identity and directory management |
| Status | Planned |

### Planned Functions

Active Directory will support:

- 40 unique fictional employee identities
- Computer accounts
- Organizational Units
- Security groups
- Authentication
- Authorization
- Group Policy
- Administrative delegation
- Role-based access
- Employee onboarding
- Employee role changes
- Employee offboarding

The Active Directory domain namespace will be selected during directory and network design.

---

## SW-005 — Windows Server DNS

| Attribute | Information |
| --- | --- |
| Software ID | `SW-005` |
| Category | Network Service |
| Product | Microsoft DNS Server |
| Host | `SLS-DC01` |
| Function | Internal DNS |
| Status | Planned |

### Planned Functions

DNS will support:

- Active Directory
- Internal hostname resolution
- Domain controllers
- Domain-joined workstations
- Internal services
- External DNS resolution through the selected DNS architecture

---

## SW-006 — Microsoft Windows 11

| Attribute | Information |
| --- | --- |
| Software ID | `SW-006` |
| Category | Endpoint Operating System |
| Product | Microsoft Windows 11 |
| Planned Hosts | `SLS-WS01`, `SLS-WS02`, `SLS-WS03` |
| Function | Organizational endpoint operating system |
| Status | Planned |

### Planned Roles

Windows 11 will provide the operating system for the initial simulated Stoneleaf Services workstations.

The initial systems will represent:

- `SLS-WS01` — Investigations
- `SLS-WS02` — Intelligence and Analysis
- `SLS-WS03` — Management and Administration

Windows workstations will eventually support:

- Domain membership
- Domain authentication
- Group Policy
- Role-based access
- Administrative tools
- Security controls
- Logging
- Troubleshooting
- Specialized applications appropriate to their assigned functions

---

## SW-007 — Ubuntu Server

| Attribute | Information |
| --- | --- |
| Software ID | `SW-007` |
| Category | Server Operating System |
| Product | Ubuntu Server 24.04 LTS |
| Planned Hostname | `SLS-LNX01` |
| Function | Linux server administration |
| Status | Planned |

### Planned Functions

Ubuntu Server will support development and demonstration of:

- Linux command-line administration
- TCP/IP configuration
- DNS configuration
- SSH
- User management
- Group management
- File ownership
- File permissions
- Package management
- Process management
- Service management
- Storage administration
- Logging
- Linux firewall configuration
- Security hardening
- Scripting
- Automation
- Troubleshooting

---

# Administrative and Troubleshooting Software

## SW-008 — PowerShell

| Attribute | Information |
| --- | --- |
| Software ID | `SW-008` |
| Category | Administration / Automation |
| Product | Microsoft PowerShell |
| Function | Windows administration, automation, and troubleshooting |
| Status | Planned / Available |

PowerShell will support:

- Windows administration
- Active Directory administration
- Network troubleshooting
- System information collection
- Automation
- Security administration
- Log analysis
- Microsoft cloud administration

---

## SW-009 — OpenSSH

| Attribute | Information |
| --- | --- |
| Software ID | `SW-009` |
| Category | Remote Administration |
| Product | OpenSSH |
| Function | Secure remote administration |
| Status | Planned |

OpenSSH will primarily support remote administration of Linux systems.

---

## SW-010 — Wireshark

| Attribute | Information |
| --- | --- |
| Software ID | `SW-010` |
| Category | Network Analysis |
| Product | Wireshark |
| Function | Packet capture and protocol analysis |
| Status | Planned |

Wireshark will support:

- Network troubleshooting
- TCP/IP analysis
- DNS analysis
- DHCP analysis
- Protocol analysis
- Traffic inspection
- Security exercises
- Incident investigation

Packet capture activities will be limited to systems and networks Stoneleaf Services is authorized to monitor.

---

# Documentation and Development Software

## SW-011 — Git

| Attribute | Information |
| --- | --- |
| Software ID | `SW-011` |
| Category | Version Control |
| Product | Git |
| Function | Version control |
| Status | Active / Planned |

Git will support version control for:

- Documentation
- Scripts
- Configuration examples
- Project files
- Portfolio materials

---

## SW-012 — GitHub

| Attribute | Information |
| --- | --- |
| Software ID | `SW-012` |
| Category | Repository / Portfolio |
| Product | GitHub |
| Function | Stoneleaf Services technical repository |
| Status | Active |

### Current Use

GitHub currently serves as the public technical documentation and portfolio platform for Stoneleaf Services.

The repository includes or will include:

- Foundation documentation
- Network design
- VMware documentation
- pfSense documentation
- Windows Server documentation
- Windows client documentation
- Linux documentation
- Security documentation
- Logging and monitoring projects
- Troubleshooting labs
- Sanitized incident reports
- Azure and Entra projects
- Project documentation
- Diagrams
- Templates

Sensitive information must not be committed to the public repository.

---

## SW-013 — Microsoft Word

| Attribute | Information |
| --- | --- |
| Software ID | `SW-013` |
| Category | Documentation |
| Product | Microsoft Word |
| Function | Detailed technical runbooks and documentation |
| Status | Active |

Microsoft Word will be used for detailed private documentation including:

- Installation runbooks
- Configuration runbooks
- Step-by-step procedures
- Screenshots
- Troubleshooting procedures
- Administrative procedures
- Project documentation

GitHub documentation will provide polished and sanitized portfolio-facing documentation where appropriate.

---

## SW-014 — Microsoft OneDrive

| Attribute | Information |
| --- | --- |
| Software ID | `SW-014` |
| Category | Cloud Storage |
| Product | Microsoft OneDrive |
| Capacity | 1 TB |
| Function | Documentation and cloud file storage |
| Status | Active |

OneDrive may support:

- Stoneleaf Services documentation
- Runbooks
- Project files
- Supporting technical materials
- Backup copies of appropriate documents

OneDrive does not eliminate the requirement for an independent backup strategy.

---

# Microsoft Cloud Platform

## SW-015 — Microsoft Azure

| Attribute | Information |
| --- | --- |
| Software ID | `SW-015` |
| Category | Cloud Platform |
| Product | Microsoft Azure |
| Function | Future cloud and hybrid infrastructure |
| Status | Planned / Available |

Stoneleaf Services currently has access to Azure resources for educational and lab development.

Future Azure activities may include:

- Virtual networks
- Subnets
- Virtual machines
- Storage
- Network security
- Monitoring
- Logging
- Identity integration
- Cloud security
- Hybrid connectivity

Cloud resources must be deployed with attention to cost and security.

---

## SW-016 — Microsoft Entra ID

| Attribute | Information |
| --- | --- |
| Software ID | `SW-016` |
| Category | Cloud Identity |
| Product | Microsoft Entra ID |
| Function | Cloud identity and access management |
| Status | Planned |

Future capabilities may include:

- Cloud identities
- Groups
- Role-Based Access Control
- Multifactor authentication
- Administrative roles
- Identity security
- Access management
- Hybrid identity

The relationship between Active Directory and Entra ID will be designed during the hybrid-infrastructure phase.

---

# Security Software

## Security Tool Selection

Stoneleaf Services will progressively introduce security tools as the infrastructure develops.

Security software should be selected according to documented requirements rather than installing large numbers of unrelated tools.

Future categories may include:

- Endpoint security
- Vulnerability assessment
- Log analysis
- Security monitoring
- SIEM
- Network analysis
- Identity security
- Cloud security
- Incident response
- Threat analysis

Individual security products will be added to the inventory when selected for implementation.

---

# Microsoft Security Technologies

Stoneleaf Services may progressively incorporate Microsoft security technologies as Microsoft and cloud capabilities develop.

Potential technologies may include:

- Microsoft Defender
- Microsoft Defender for Endpoint
- Microsoft Sentinel
- Microsoft security portals
- Kusto Query Language (KQL)
- Entra security capabilities

These technologies are not considered fully implemented merely because they appear in this future-development section.

Each product should receive its own software inventory entry when it becomes part of the operational lab.

---

# Digital Investigation and Forensics Software

Stoneleaf Services will eventually require software supporting digital investigation and forensic exercises.

Potential capability categories include:

- Disk analysis
- File-system analysis
- Memory analysis
- Timeline analysis
- Log analysis
- Metadata analysis
- Network analysis
- Artifact collection
- Evidence organization
- Reporting

Specific products will be selected during the digital-investigation development phase.

Software should not be added solely because it is commonly associated with digital forensics.

Each tool must support a defined capability or training objective.

---

# Intelligence and OSINT Software

Stoneleaf Services will eventually require tools supporting intelligence collection and analysis.

Potential capability categories include:

- Open-source research
- Information collection
- Source evaluation
- Information verification
- Data organization
- Timeline analysis
- Link analysis
- Relationship analysis
- Analytical writing
- Reporting

Specific products will be selected when the associated requirements and workflows are defined.

Tools must be used within applicable legal, ethical, authorization, privacy, and platform requirements.

---

# Temporary Security and Testing Systems

Not every operating system or security platform used in Stoneleaf Services exercises requires permanent deployment.

Temporary virtual machines may be created when required for:

- Cybersecurity exercises
- Security testing
- Troubleshooting
- Training
- Incident-response exercises
- Digital investigations
- Tool evaluation

Examples may eventually include specialized Linux or security distributions.

Temporary systems should not become permanent infrastructure unless a documented requirement justifies the change.

---

# Software Licensing

Stoneleaf Services software must be used according to applicable licensing requirements.

Software inventory records should eventually identify where applicable:

- Product
- Edition
- Version
- License type
- Subscription status
- Educational licensing
- Trial licensing
- Open-source licensing
- Renewal requirements

License keys and other sensitive licensing information must not be stored in the public GitHub repository.

---

# Software Version Management

Exact software versions should be documented when systems are deployed.

Version information is important for:

- Compatibility
- Security
- Troubleshooting
- Reproducibility
- Vulnerability management
- Patch management
- Technical documentation

Software versions should be updated when major upgrades occur.

---

# Patch and Update Management

Stoneleaf Services must maintain software through appropriate patching and update processes.

Software requiring regular maintenance includes:

- Host operating systems
- VMware
- pfSense
- Windows Server
- Windows workstations
- Ubuntu Server
- Administrative utilities
- Security tools
- Investigation tools
- Cloud management tools

Updates should be validated when they have the potential to affect important lab functionality.

---

# Software Security

Stoneleaf Services software should be obtained from trusted sources.

Software installation practices should include:

- Vendor or project verification
- Version documentation
- License review where appropriate
- Security updates
- Removal of unnecessary software
- Avoidance of untrusted software sources
- Documentation of significant software installations

Credentials, API keys, tokens, license keys, private keys, and other secrets must not be stored in the public repository.

---

# Software Selection Principles

New software should be introduced when it satisfies one or more documented requirements.

Selection criteria should include:

- Technical capability
- Security
- Compatibility
- Cost
- Licensing
- Hardware requirements
- Training value
- Professional relevance
- Documentation quality
- Long-term maintainability
- Integration with existing Stoneleaf Services infrastructure

Software should not be installed simply to increase the number of technologies represented in the lab.

---

# Current Core Software Baseline

| Software ID | Technology | Primary Function | Status |
| --- | --- | --- | --- |
| `SW-001` | VMware | Virtualization | Active / Planned |
| `SW-002` | pfSense | Firewall, routing, DHCP, NAT | Planned |
| `SW-003` | Windows Server | Server operating system | Planned |
| `SW-004` | Active Directory Domain Services | Identity and directory services | Planned |
| `SW-005` | Windows Server DNS | Internal DNS | Planned |
| `SW-006` | Windows 11 | Endpoint operating system | Planned |
| `SW-007` | Ubuntu Server 24.04 LTS | Linux server | Planned |
| `SW-008` | PowerShell | Administration and automation | Planned / Available |
| `SW-009` | OpenSSH | Remote administration | Planned |
| `SW-010` | Wireshark | Network analysis | Planned |
| `SW-011` | Git | Version control | Active / Planned |
| `SW-012` | GitHub | Repository and portfolio | Active |
| `SW-013` | Microsoft Word | Detailed documentation | Active |
| `SW-014` | Microsoft OneDrive | Cloud file storage | Active |
| `SW-015` | Microsoft Azure | Cloud infrastructure | Planned / Available |
| `SW-016` | Microsoft Entra ID | Cloud identity | Planned |

---

# Future Software Expansion

The software inventory is expected to expand as Stoneleaf Services develops additional capabilities.

Future categories may include:

### Infrastructure

- Additional server roles
- Backup software
- Storage management
- Network monitoring
- Infrastructure monitoring

### Cybersecurity

- SIEM
- Endpoint detection and response
- Vulnerability management
- Security monitoring
- Threat-analysis tools
- Cloud-security tools

### Digital Investigations

- Digital-forensics platforms
- Artifact-analysis tools
- Timeline tools
- Memory-analysis tools
- Evidence-management tools

### Intelligence and Analysis

- OSINT tools
- Link-analysis tools
- Research-management tools
- Data-analysis tools
- Visualization tools
- Reporting tools

### Automation and Development

- Scripting environments
- Development tools
- Infrastructure automation
- APIs
- Configuration-management tools

Products will be added when specific requirements justify their deployment.

---

# Inventory Maintenance

The Software Inventory is a living document.

It should be updated when:

- Software is installed
- Software is removed
- A new platform is selected
- Major versions change
- Licensing changes
- Software changes operational role
- Software is retired
- New Stoneleaf Services capabilities are developed

Planned software should not be represented as operational until deployment and validation are complete.

---

# Current Status

**Inventory Status:** Initial Baseline

**Current Phase:** Foundation Planning and Documentation

The current software baseline establishes the technologies required to begin building the Stoneleaf Services infrastructure while preserving room for cybersecurity, investigation, intelligence, cloud, and business capabilities to expand over time.

---

# Next Foundation Document

The next Foundation document is:

**`Naming-Standards.md`**

The Naming Standards document will establish consistent naming rules for Stoneleaf Services systems, users, administrative accounts, groups, Organizational Units, network objects, documentation, projects, and other technical resources.

The naming standard will also provide the framework we will later use when creating the **40 individual fictional employee identities and their associated accounts**.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
