# 00 — Foundation

## Stoneleaf Services

**No Stone Left Unturned**

The Foundation section establishes the organizational, technical, and documentation standards that guide the development of Stoneleaf Services.

Before infrastructure is deployed, the requirements, naming conventions, documentation practices, hardware resources, software platforms, and change-management processes are defined here.

The purpose of this section is to ensure that the Stoneleaf Services environment is built intentionally and consistently rather than as a collection of unrelated systems.

---

## Foundation Status

**Version:** 1.0  
**Status:** Complete  
**Completed:** September 2026  
**Next Phase:** `01-Network-Design`

The initial Stoneleaf Services Foundation has been established.

The Foundation defines the organizational purpose, lab scope, business and technical requirements, hardware and software inventories, identity structure, naming standards, documentation standards, and change-management process required to begin technical architecture and design.

Foundation documentation remains subject to controlled revision as Stoneleaf Services develops. Future changes will be documented according to the Stoneleaf Services change-management process.

---

## Objectives

The Foundation phase establishes the baseline for all future Stoneleaf Services projects and infrastructure.

The primary objectives are to:

- Define the purpose and scope of Stoneleaf Services.
- Establish business and technical requirements.
- Document available hardware and software resources.
- Establish system and device naming conventions.
- Define documentation standards.
- Establish basic change-management procedures.
- Create repeatable standards for future infrastructure deployments.
- Maintain consistency as the environment expands.
- Support systematic troubleshooting and root-cause analysis.
- Provide documentation suitable for a professional technical portfolio.

---

## Foundation Documents

| Document | Purpose | Status |
| --- | --- | --- |
| `Organization-Overview.md` | Defines the organization, mission, development strategy, and long-term direction | Complete |
| `Lab-Scope.md` | Defines the purpose, boundaries, systems, and objectives of the lab environment | Complete |
| `Business-Requirements.md` | Defines the organizational capabilities the environment must support | Complete |
| `Technical-Requirements.md` | Translates business requirements into technical capabilities | Complete |
| `Hardware-Inventory.md` | Documents current and planned physical hardware resources | Complete |
| `Software-Inventory.md` | Documents current and planned software platforms | Complete |
| `Naming-Standards.md` | Establishes naming conventions for systems, identities, groups, records, and documentation | Complete |
| `Documentation-Standards.md` | Establishes documentation, runbook, troubleshooting, change, incident, and investigation standards | Complete |
| `Change-Management.md` | Establishes the process for planning, implementing, validating, and recording technical changes | Complete |
| `Identity-Roster.md` | Defines the 40 synthetic Stoneleaf Services employee identities and organizational relationships | Complete |

---

## Design Principles

### Documentation First

Infrastructure should be designed and documented before deployment whenever practical.

Major systems should have documented:

- Purpose
- Requirements
- Dependencies
- Configuration
- Installation procedures
- Validation procedures
- Troubleshooting procedures
- Security considerations
- Change history

### Standardization

Systems will follow consistent naming, addressing, configuration, and documentation standards.

Standardization makes the environment easier to administer, expand, secure, and troubleshoot.

### Separation of Responsibilities

Infrastructure services should have clearly defined responsibilities.

The initial division of responsibilities includes:

- **pfSense** — Firewall, routing, DHCP, NAT, and VPN services
- **Windows Server** — Active Directory Domain Services and DNS
- **Ubuntu Server** — Linux server administration and services
- **Windows workstations** — Management, investigation, intelligence, and analysis endpoints
- **VMware** — Virtualization platform
- **Microsoft Azure and Microsoft Entra ID** — Future cloud and hybrid infrastructure

Clearly defined responsibilities make dependencies easier to understand and failures easier to isolate during troubleshooting.

### Security by Design

Security considerations should be incorporated during design and implementation rather than added only after deployment.

This includes:

- Least privilege
- Identity and access management
- Network segmentation
- Secure administrative practices
- System hardening
- Patch management
- Logging and monitoring
- Configuration management
- Credential protection
- Protection of sensitive information

### Troubleshooting by Design

A major purpose of the Stoneleaf Services environment is the development of systematic troubleshooting and root-cause analysis skills.

The environment will eventually support troubleshooting exercises involving:

- TCP/IP
- Network connectivity
- DHCP
- DNS
- Routing
- NAT
- Firewall rules
- Active Directory
- Authentication and authorization
- Group Policy
- Windows services
- Linux services
- Logging and monitoring
- Cloud connectivity
- Security controls

Troubleshooting activities will document the initial symptoms, evidence collected, hypotheses tested, root cause, corrective action, and final validation.

---

## Initial On-Premises Infrastructure

The initial Stoneleaf Services environment is designed around a virtualized small-business network.

| Hostname | Platform | Primary Role |
| --- | --- | --- |
| `SLS-FW01` | pfSense | Firewall, router, DHCP, NAT |
| `SLS-DC01` | Windows Server | Active Directory Domain Services and DNS |
| `SLS-LNX01` | Ubuntu Server 24.04 LTS | Linux server administration and services |
| `SLS-WS01` | Windows 11 | Investigations workstation |
| `SLS-WS02` | Windows 11 | Intelligence and analysis workstation |
| `SLS-WS03` | Windows 11 | Management and administrative workstation |

VMware will provide the initial virtualization platform for the on-premises environment.

Microsoft Azure and Microsoft Entra ID are planned for a later phase to extend Stoneleaf Services into a hybrid environment.

---

## Documentation Model

Stoneleaf Services uses two complementary forms of documentation.

### GitHub Documentation

This repository contains portfolio-appropriate technical documentation, including:

- Architecture documentation
- Design decisions
- Network and system diagrams
- Standards
- Sanitized configurations
- Technical procedures
- Troubleshooting exercises
- Incident reports
- Project documentation
- Lessons learned

### Detailed Build Runbooks

Detailed step-by-step build instructions are maintained separately from the public repository.

These runbooks will document procedures such as:

- VMware installation and configuration
- VMware virtual networking
- Virtual machine creation
- pfSense installation and configuration
- Windows Server installation
- Active Directory deployment
- DNS configuration
- Windows workstation deployment
- Ubuntu Server deployment
- Security configuration
- Logging and monitoring
- Azure and Entra ID configuration
- Verification procedures
- Troubleshooting procedures

The runbooks are intended to make the Stoneleaf Services environment reproducible from initial deployment through final validation.

---

## Security and Repository Hygiene

The Stoneleaf Services repository will not intentionally contain:

- Passwords
- Authentication credentials
- API keys
- Authentication tokens
- Private cryptographic keys
- Personally identifiable information
- Confidential client information
- Sensitive investigation information
- Unredacted security-sensitive configuration information
- Virtual machine images
- Proprietary software
- Operating system installation media

Configurations, screenshots, investigation exercises, and other materials published to the repository will be reviewed and sanitized when necessary.

---

## Current Status

**Phase:** Foundation Planning and Documentation

The Stoneleaf Services environment is currently being designed and documented prior to full deployment.

The immediate objective is to complete the Foundation documentation before proceeding to detailed network design and infrastructure deployment.

---

## Next Phase

Completion of the Foundation phase will establish the requirements and standards necessary to begin:

**`01-Network-Design`**

The Network Design phase will define:

- Network topology
- IP addressing
- Subnets
- Static addressing
- DHCP architecture
- DNS architecture
- Default gateways
- Routing
- NAT
- Firewall placement
- VMware virtual networking
- Traffic flows
- Future network segmentation
- Future hybrid connectivity

---

**Stoneleaf Services**  
*No Stone Left Unturned*
