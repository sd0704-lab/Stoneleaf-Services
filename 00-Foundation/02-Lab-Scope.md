# Stoneleaf Services — Home Lab Scope

**No Stone Left Unturned**

## Purpose

The Stoneleaf Services home lab is a controlled technical environment designed to develop, practice, test, document, and demonstrate practical skills in information technology, networking, systems administration, cybersecurity, digital investigations, intelligence support, and technical analysis.

The lab is intended to simulate a small organizational IT environment rather than function solely as a collection of independent virtual machines.

Systems within the environment will interact through defined network, identity, security, administrative, and logging architectures.

The environment will be used to design infrastructure, deploy systems, administer services, implement security controls, generate realistic technical problems, troubleshoot failures, investigate incidents, and document findings.

---

## Primary Objectives

The Stoneleaf Services home lab will provide practical experience in the following areas:

- Network design
- TCP/IP
- IP addressing and subnetting
- Routing
- DHCP
- DNS
- Network Address Translation (NAT)
- Firewall administration
- Virtual networking
- Virtualization
- Windows administration
- Windows Server administration
- Active Directory Domain Services
- Group Policy
- Linux server administration
- Identity and access management
- Microsoft Azure
- Microsoft Entra ID
- Cloud and hybrid infrastructure
- Cybersecurity operations
- System hardening
- Security monitoring
- Centralized logging
- Incident detection
- Incident response
- Digital investigations
- Digital forensics
- Open-source intelligence support
- Technical analysis
- Troubleshooting
- Root-cause analysis
- Technical documentation

---

## Lab Model

The lab will simulate a small organization with on-premises infrastructure and future cloud integration.

The environment will initially consist of virtual machines hosted through VMware on locally owned hardware.

The initial architecture will contain:

| Hostname | Platform | Primary Role |
| --- | --- | --- |
| `SLS-FW01` | pfSense | Firewall, router, DHCP, NAT |
| `SLS-DC01` | Windows Server | Active Directory Domain Services and DNS |
| `SLS-LNX01` | Ubuntu Server 24.04 LTS | Linux server administration and services |
| `SLS-WS01` | Windows 11 | Investigations workstation |
| `SLS-WS02` | Windows 11 | Intelligence and analysis workstation |
| `SLS-WS03` | Windows 11 | Management and administrative workstation |

Additional systems may be introduced when they support a documented learning, operational, security, investigation, or testing requirement.

Systems should not be added solely to increase the size or complexity of the lab.

---

## Virtualization Scope

VMware will provide the initial virtualization platform for the Stoneleaf Services on-premises environment.

Virtualization activities will include:

- VMware configuration
- Virtual machine creation
- Virtual CPU allocation
- Virtual memory allocation
- Virtual storage allocation
- Virtual network adapters
- Virtual network configuration
- VM snapshots where appropriate
- VM backup and recovery concepts
- Resource management
- Virtual machine troubleshooting

Detailed procedures will be developed so that the environment can be reproduced from documentation.

---

## Network Scope

The Stoneleaf Services network will be designed as a controlled private network.

The networking environment will include:

- Private IPv4 addressing
- Subnetting
- Static addressing
- Dynamic addressing
- DHCP
- DNS
- Default gateways
- Routing
- NAT
- Firewall rules
- Network access control
- Virtual network adapters
- VMware virtual networking
- Internet connectivity
- Network troubleshooting

The initial network will begin with a relatively simple architecture.

Additional segmentation and VLANs may be introduced later as the environment grows and the technical requirements justify additional complexity.

---

## pfSense Scope

`SLS-FW01` will serve as the primary network edge device for the Stoneleaf Services lab.

Its planned responsibilities include:

- Firewall services
- Routing
- DHCP
- Network Address Translation
- Internet connectivity
- Traffic control
- Network security policy enforcement
- Logging
- VPN capabilities when implemented
- Future inter-network routing
- Future network segmentation

pfSense will provide a central location for learning how traffic moves between internal systems and external networks.

---

## Windows Server Scope

`SLS-DC01` will provide centralized Windows identity and name-resolution services.

Its planned responsibilities include:

- Active Directory Domain Services
- DNS
- Domain authentication
- Computer accounts
- User accounts
- Security groups
- Organizational Units
- Group Policy
- Administrative delegation
- Identity management
- Access-control testing
- Windows event logging
- Active Directory troubleshooting

The domain controller will use a static IP address.

DHCP will remain a pfSense responsibility unless a future lab exercise specifically requires testing Windows Server DHCP.

---

## Windows Workstation Scope

Three Windows workstations will initially represent different organizational functions.

### SLS-WS01 — Investigations

This workstation will support the development of digital investigation and related technical capabilities.

Potential future activities include:

- Evidence review
- Log analysis
- Timeline analysis
- Digital forensics exercises
- Incident investigation
- Research
- Documentation
- Investigation reporting

### SLS-WS02 — Intelligence and Analysis

This workstation will support intelligence-related research and analytical exercises.

Potential future activities include:

- Open-source research
- Information collection
- Source evaluation
- Information verification
- Timeline development
- Link analysis
- Intelligence analysis
- Analytical reporting

### SLS-WS03 — Management and Administration

This workstation will represent an administrative and management endpoint.

Potential activities include:

- Business administration
- Documentation
- Infrastructure administration
- Remote administration
- Policy management
- Project management
- Administrative testing

The workstations will also provide multiple endpoints for testing networking, Active Directory, Group Policy, permissions, security controls, and troubleshooting scenarios.

---

## Linux Scope

`SLS-LNX01` will run Ubuntu Server 24.04 LTS.

The Linux environment will be used to develop practical experience with:

- Command-line administration
- SSH
- Linux networking
- Users and groups
- File ownership
- File permissions
- Package management
- Service management
- Process management
- Storage
- Linux logs
- Firewall configuration
- Remote administration
- System hardening
- Scripting and automation
- Troubleshooting

Additional Linux services may be deployed as specific requirements are identified.

---

## Cloud and Hybrid Scope

The initial Stoneleaf Services deployment will focus on the on-premises environment.

Microsoft Azure and Microsoft Entra ID will be introduced after the core on-premises environment is functional and documented.

Future cloud and hybrid activities may include:

- Microsoft Entra ID
- Azure virtual networks
- Azure virtual machines
- Azure storage
- Azure identity management
- Role-Based Access Control
- Cloud logging
- Cloud monitoring
- Azure security controls
- Hybrid identity
- Secure connectivity between environments
- Site-to-site VPN concepts
- Cloud troubleshooting

Cloud resources will be deployed deliberately with consideration for cost, security, and learning objectives.

---

## Cybersecurity Scope

The Stoneleaf Services lab will provide a controlled environment for developing defensive cybersecurity capabilities.

Activities may include:

- System hardening
- Network security
- Identity security
- Access control
- Vulnerability identification
- Patch management
- Security monitoring
- Log analysis
- Endpoint monitoring
- Network traffic analysis
- Incident detection
- Incident response
- Threat analysis
- Security configuration
- Security validation
- Security troubleshooting

Additional cybersecurity tools will be introduced when they support specific documented objectives.

---

## Logging and Monitoring Scope

Logging will eventually be treated as a core infrastructure capability rather than an optional feature.

The environment will generate and analyze logs from sources such as:

- pfSense
- Windows Server
- Active Directory
- DNS
- Windows workstations
- Ubuntu Server
- Authentication systems
- Security tools
- Azure resources

Future development may include centralized log collection and security monitoring platforms.

The objective is to understand not only how systems operate normally, but how their behavior is represented through logs and telemetry.

---

## Troubleshooting Scope

Troubleshooting is one of the primary purposes of the Stoneleaf Services home lab.

The environment will be used to create and investigate failures involving:

- Incorrect IP configuration
- DHCP failures
- DNS failures
- Default gateway problems
- Routing failures
- NAT failures
- Firewall rules
- Network connectivity
- Domain connectivity
- Active Directory
- Authentication
- Authorization
- Group Policy
- Windows services
- Linux services
- Permissions
- Cloud connectivity
- Security controls

Troubleshooting exercises should follow a structured methodology and be documented.

Each exercise should identify:

1. Problem statement
2. Observed symptoms
3. Scope
4. Evidence collected
5. Initial hypotheses
6. Tests performed
7. Results
8. Root cause
9. Corrective action
10. Validation
11. Lessons learned

---

## Investigation Scope

The lab will eventually support simulated digital investigation and incident-response exercises.

Investigation activities may include:

- Log review
- Event correlation
- Timeline development
- Network traffic analysis
- File-system analysis
- Endpoint investigation
- Account activity review
- Incident reconstruction
- Evidence documentation
- Report writing

Investigation exercises will use authorized lab systems and simulated, generated, sanitized, or otherwise appropriate data.

---

## Intelligence and Analysis Scope

The lab may also support the technical components of intelligence collection and analysis development.

Potential activities include:

- Open-source intelligence
- Public-source research
- Source evaluation
- Information verification
- Collection planning
- Data organization
- Timeline analysis
- Link and relationship analysis
- Pattern identification
- Analytical writing
- Intelligence reporting

These capabilities will be developed progressively and separately from the administration of the core IT infrastructure.

---

## Documentation Scope

Documentation is considered a core component of the Stoneleaf Services environment.

Documentation will include:

- Requirements
- Architecture
- Network diagrams
- IP addressing
- Naming standards
- Build procedures
- Configuration procedures
- Security procedures
- Validation procedures
- Troubleshooting procedures
- Change records
- Incident reports
- Investigation reports
- Project documentation
- Lessons learned

Detailed step-by-step implementation runbooks will be maintained separately where appropriate.

GitHub will contain portfolio-appropriate documentation and sanitized technical material.

---

## In-Scope Activities

The following activities are considered within the intended scope of the lab:

- Designing infrastructure
- Deploying virtual machines
- Configuring networks
- Administering systems
- Managing identities
- Implementing security controls
- Monitoring systems
- Collecting logs
- Troubleshooting failures
- Simulating incidents
- Investigating simulated incidents
- Performing authorized security testing
- Practicing digital forensics
- Conducting lawful open-source research
- Developing analytical products
- Automating administrative tasks
- Documenting technical work

---

## Out-of-Scope Activities

The following activities are outside the intended scope of the Stoneleaf Services home lab:

- Unauthorized access to third-party systems
- Testing systems without authorization
- Collection of unlawfully obtained information
- Deployment of malicious software outside controlled lab exercises
- Storage of real client information without appropriate safeguards
- Storage of real credentials in public repositories
- Publication of sensitive configuration information
- Unlawful surveillance
- Unauthorized interception of communications
- Activities outside applicable laws, authorization, or professional standards

The lab is intended to provide a controlled environment in which technical and investigative skills can be developed safely and lawfully.

---

## Resource Constraints

The Stoneleaf Services lab is designed around available personal computing resources.

Resource constraints may include:

- CPU capacity
- Memory
- SSD capacity
- Backup storage
- Internet bandwidth
- Cloud-service costs
- Software licensing

Systems will therefore be added based on documented requirements rather than simply maximizing the number of virtual machines.

Virtual machines may be powered on only when required for a particular exercise or service.

---

## Current Deployment Constraint

The Stoneleaf Services environment is currently in the planning and documentation phase.

Full virtual machine deployment and expansion are being deferred until sufficient local SSD capacity is available.

During this period, development will focus on:

- Architecture
- Requirements
- Documentation
- Network design
- Implementation runbooks
- VMware deployment procedures
- System build procedures
- Security planning
- Troubleshooting scenarios

This approach allows the environment to be thoroughly planned before additional storage is installed and full deployment begins.

---

## Scope Expansion

The scope of the Stoneleaf Services home lab is expected to evolve.

New systems, technologies, and capabilities should be added when they satisfy at least one of the following conditions:

- Support a defined learning objective
- Support a professional certification objective
- Support an identified Stoneleaf Services capability
- Improve the realism of the environment
- Provide a meaningful troubleshooting opportunity
- Support cybersecurity development
- Support investigation or analysis development
- Support a documented project requirement

Significant changes to the scope should be documented through the Stoneleaf Services change-management process.

---

## Success Criteria

The Stoneleaf Services home lab will be considered successful when it provides a reproducible environment in which the following can be demonstrated:

- Infrastructure can be deployed from documentation.
- Systems can communicate according to the network design.
- Clients can receive correct network configuration.
- Internal DNS functions correctly.
- Windows systems can authenticate through Active Directory.
- Administrative policies can be centrally managed.
- Linux systems can be securely administered.
- Network traffic can be controlled and observed.
- Security events can be logged and investigated.
- Failures can be systematically diagnosed.
- Root causes can be identified and corrected.
- Changes can be documented and validated.
- Simulated incidents can be investigated.
- Technical findings can be communicated through professional documentation.
- The environment can expand into cloud and hybrid infrastructure without abandoning established standards.

---

## Current Status

**Phase:** Foundation Planning and Documentation

**Deployment Status:** Full deployment deferred pending storage expansion.

**Current Priority:** Complete the Stoneleaf Services Foundation documentation and implementation runbooks before beginning full infrastructure deployment.

---

## Next Foundation Document

Following completion of the Home Lab Scope, the next Foundation document is:

**`Business-Requirements.md`**

This document will define what Stoneleaf Services requires the technical environment to accomplish from an organizational and capability perspective.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
