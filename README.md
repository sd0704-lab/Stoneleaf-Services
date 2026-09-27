# Stoneleaf Services

**No Stone Left Unturned**

Stoneleaf Services is a developing IT, cybersecurity, digital investigations, intelligence collection, and analysis project built around a practical hybrid home-lab environment.

This repository documents the design, implementation, administration, security, troubleshooting, and continued development of the Stoneleaf Services technical environment. The project is intended to provide hands-on experience with real-world technologies while creating a documented portfolio of technical and analytical skills.

## Project Objectives

Stoneleaf Services is being developed to build practical experience in:

- Network design and administration
- Network troubleshooting
- Firewall configuration and management
- Windows Server administration
- Active Directory Domain Services
- DNS and DHCP
- Windows endpoint administration
- Linux server administration
- Virtualization
- Microsoft Azure
- Microsoft Entra ID
- Cybersecurity operations
- Security monitoring and logging
- Incident response
- Digital forensics and investigations
- Open-source intelligence (OSINT)
- Intelligence collection and analysis
- Technical documentation
- Root-cause analysis and systematic troubleshooting

The environment will grow as new technical skills and capabilities are developed.

## Current Environment

The initial Stoneleaf Services on-premises environment is designed around a virtualized small-business network.

### Core Infrastructure

| System | Platform | Primary Role |
| --- | --- | --- |
| SLS-FW01 | pfSense | Firewall, routing, DHCP, NAT, and network security |
| SLS-DC01 | Windows Server | Active Directory Domain Services and DNS |
| SLS-LNX01 | Ubuntu Server 24.04 LTS | Linux server administration and services |
| SLS-WS01 | Windows 11 | Investigations workstation |
| SLS-WS02 | Windows 11 | Intelligence and analysis workstation |
| SLS-WS03 | Windows 11 | Management and administrative workstation |

VMware is used to virtualize the on-premises environment.

Future development will include Microsoft Azure and Microsoft Entra ID to create a hybrid environment.

## Project Development

Stoneleaf Services is being developed in phases.

1. Documentation and project standards
2. Business and technical requirements
3. Network architecture and IP addressing
4. VMware virtual infrastructure
5. pfSense firewall and routing
6. Windows Server, Active Directory, and DNS
7. Windows client deployment and domain integration
8. Ubuntu Server deployment and administration
9. Security hardening
10. Centralized logging and monitoring
11. Troubleshooting and incident-response exercises
12. Azure and Entra ID integration
13. Digital investigation and intelligence capabilities

Each phase will include planning, implementation procedures, validation, troubleshooting, and lessons learned.

## Repository Structure

```text
Stoneleaf-Services/
│
├── 00-Foundation/
├── 01-Network-Design/
├── 02-VMware/
├── 03-pfSense/
├── 04-Windows-Server/
├── 05-Windows-Clients/
├── 06-Linux/
├── 07-Security/
├── 08-Logging-Monitoring/
├── 09-Troubleshooting-Labs/
├── 10-Incident-Reports/
├── 11-Azure-Entra/
├── 12-Projects/
├── diagrams/
├── templates/
├── assets/
└── README.md
