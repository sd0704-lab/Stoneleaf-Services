# Stoneleaf Services — Business Requirements

**No Stone Left Unturned**

## Purpose

This document defines the business and organizational requirements that drive the design of the Stoneleaf Services technical environment.

Business requirements describe what the organization requires from its technology environment without prescribing the specific technical implementation used to satisfy those requirements.

Detailed technical solutions, configurations, addressing, software selections, and implementation procedures are defined in subsequent technical and design documentation.

---

## Organizational Model

The Stoneleaf Services home lab will simulate the technology requirements of a small professional services organization.

The simulated organization will consist of:

- **40 individual employees**
- Multiple organizational departments and functions
- Management and supervisory relationships
- Technical and non-technical personnel
- Standard and privileged users
- Different information-access requirements
- Different security requirements
- Different workstation and application requirements

Each simulated employee will have an individual fictional identity rather than a generic numbered user account.

All employee identities used within the lab are synthetic and exist solely for training, testing, administration, cybersecurity, investigation, and analytical exercises.

---

## BR-01 — Individual Employee Identities

Stoneleaf Services requires the environment to support **40 unique simulated employee identities**.

Each employee will eventually have documented attributes including:

- First name
- Last name
- Employee ID
- Job title
- Department
- Manager
- Employment role
- Username
- Organizational email address
- User Principal Name (UPN)
- Active Directory account
- Organizational Unit placement
- Security-group membership
- Access requirements
- Privilege level
- Assigned workstation where applicable
- Cloud identity where applicable

Employee identities will be designed to represent realistic organizational relationships and access requirements.

Generic identities such as `user01` through `user40` will not be used as the primary employee accounts.

---

## BR-02 — Organizational Structure

Stoneleaf Services requires a defined organizational structure for the simulated 40-person workforce.

The structure must support:

- Executive or organizational leadership
- Management
- Information technology
- Cybersecurity
- Investigations
- Intelligence and analysis
- Business and administrative functions
- Appropriate reporting relationships

The final organizational structure will be documented separately before employee accounts are created.

The organizational structure will be used to determine:

- Active Directory Organizational Units
- Security groups
- Access permissions
- Group Policy requirements
- Administrative responsibilities
- Information-access boundaries
- Workstation requirements
- Cloud access requirements
- Security monitoring requirements

---

## BR-03 — Centralized Identity Management

Stoneleaf Services requires centralized management of employee identities.

The organization must be able to:

- Create user accounts
- Disable user accounts
- Modify user accounts
- Reset credentials
- Assign users to organizational groups
- Control access based on job responsibilities
- Apply organizational policies
- Manage authentication
- Review account activity
- Identify privileged accounts
- Support employee onboarding
- Support employee role changes
- Support employee offboarding

Identity management must be structured so that access can be granted and removed consistently.

---

## BR-04 — Role-Based Access

Employees must receive access according to their organizational responsibilities.

Stoneleaf Services requires the ability to distinguish between:

- Standard users
- Managers
- Investigators
- Intelligence personnel
- IT personnel
- Security personnel
- Administrators
- Privileged administrators

Access should be assigned through organizational roles and groups whenever practical rather than individually configuring permissions for every employee.

The environment must support the principle of least privilege.

---

## BR-05 — Authentication

Stoneleaf Services requires employees to authenticate using individually assigned accounts.

The organization must be able to:

- Uniquely identify users
- Authenticate users
- Apply password and account policies
- Control access to organizational resources
- Identify authentication failures
- Review authentication activity
- Disable access when necessary

Shared employee accounts should be avoided except where a documented technical requirement specifically requires one.

---

## BR-06 — Network Connectivity

Stoneleaf Services requires reliable network connectivity between authorized organizational systems.

The network must support:

- Workstation-to-server communication
- Server-to-server communication
- Internet connectivity
- Internal name resolution
- Dynamic network configuration for appropriate endpoints
- Static network configuration for critical infrastructure
- Controlled communication between network resources
- Future cloud connectivity

Network connectivity must be designed so that failures can be isolated and systematically troubleshot.

---

## BR-07 — Internet Access

Authorized Stoneleaf Services systems require controlled access to external internet resources.

Internet connectivity is necessary to support activities including:

- Software updates
- Cloud services
- Technical research
- Open-source research
- Security research
- Documentation
- Vendor resources
- Training resources
- Administrative activities

Internet access must pass through organizational network security controls.

---

## BR-08 — Name Resolution

Stoneleaf Services requires reliable internal and external name resolution.

Employees and systems must be able to locate authorized organizational resources by name rather than requiring users to memorize IP addresses.

Name-resolution services must support the organization's identity infrastructure and internal systems.

---

## BR-09 — Dynamic Network Configuration

Stoneleaf Services requires automatic network configuration for appropriate endpoint devices.

Standard workstations should be capable of automatically receiving required network configuration.

Critical infrastructure systems should use controlled and predictable addressing.

---

## BR-10 — Centralized Windows Administration

Stoneleaf Services requires centralized administration of Windows systems.

The organization must be capable of centrally managing:

- User identities
- Computer identities
- Security settings
- User settings
- Authentication
- Access controls
- Organizational policies

Centralized administration should reduce the need to configure every Windows workstation independently.

---

## BR-11 — Linux Capability

Stoneleaf Services requires Linux server capability.

The environment must provide opportunities to develop and demonstrate:

- Linux administration
- Command-line operation
- Remote administration
- User and group management
- Permissions
- Networking
- Service management
- Logging
- Security
- Troubleshooting

Linux capability must coexist with the Windows environment.

---

## BR-12 — Virtualization

Stoneleaf Services requires virtualization to support the simulated organizational infrastructure.

Virtualization must allow the organization to:

- Operate multiple systems on available physical hardware
- Create isolated virtual systems
- Allocate computing resources
- Configure virtual networking
- Reproduce systems
- Test configuration changes
- Create controlled troubleshooting scenarios
- Support future security exercises

The environment should remain manageable within available hardware resources.

---

## BR-13 — Security

Stoneleaf Services requires security to be incorporated throughout the environment.

The organization must be able to:

- Control access to systems and information
- Apply least privilege
- Protect privileged accounts
- Apply security policies
- Control network traffic
- Maintain system updates
- Harden systems
- Record security-relevant events
- Detect abnormal activity
- Investigate security events
- Respond to simulated incidents

Security must be considered during system design rather than treated solely as a later addition.

---

## BR-14 — Logging

Stoneleaf Services requires systems to generate sufficient logging to support administration, troubleshooting, security monitoring, and investigations.

Relevant systems should provide records of events such as:

- Authentication
- Account activity
- System events
- Service events
- Network activity
- Firewall activity
- DNS activity
- Administrative actions
- Security events

Logging requirements will expand as the environment becomes more sophisticated.

---

## BR-15 — Monitoring

Stoneleaf Services requires the ability to monitor the health, availability, and security of important systems.

Monitoring should eventually support:

- System availability
- Service availability
- Security events
- Authentication activity
- Network activity
- Infrastructure failures
- Suspicious behavior

Centralized monitoring capabilities may be introduced as the environment matures.

---

## BR-16 — Troubleshooting

Stoneleaf Services requires the environment to support systematic technical troubleshooting.

The organization must be able to create, identify, diagnose, correct, and document failures involving areas such as:

- TCP/IP
- DHCP
- DNS
- Routing
- NAT
- Firewalls
- Windows
- Linux
- Active Directory
- Authentication
- Authorization
- Group Policy
- Services
- Permissions
- Cloud connectivity
- Security controls

Troubleshooting activities must support root-cause analysis rather than relying solely on temporary fixes.

---

## BR-17 — Change Management

Stoneleaf Services requires significant technical changes to be documented.

Changes should record information such as:

- What is changing
- Why the change is required
- Systems affected
- Risks
- Dependencies
- Planned implementation
- Validation procedures
- Rollback considerations
- Actual results
- Problems encountered
- Lessons learned

This requirement applies to infrastructure, networking, security, identity, cloud, and other significant technical changes.

---

## BR-18 — Technical Documentation

Stoneleaf Services requires documentation sufficient to understand, administer, troubleshoot, reproduce, and expand the environment.

Documentation should include:

- Requirements
- Architecture
- Network diagrams
- System inventories
- Naming conventions
- IP addressing
- Build procedures
- Configuration procedures
- Administrative procedures
- Security controls
- Troubleshooting procedures
- Change records
- Incident records
- Investigation records
- Validation results

Documentation is considered part of the implementation process.

---

## BR-19 — Reproducibility

Stoneleaf Services requires infrastructure to be reproducible from documented procedures whenever practical.

A technically competent administrator following the documentation should be able to understand:

- What must be deployed
- Why it exists
- What dependencies exist
- How it should be configured
- How proper operation is verified
- How common failures can be investigated

This requirement supports both disaster recovery concepts and professional technical documentation practices.

---

## BR-20 — Investigation Capability

Stoneleaf Services requires the environment to progressively support simulated digital investigations.

The organization should eventually be capable of conducting controlled exercises involving:

- Event review
- Log analysis
- Authentication analysis
- Network activity analysis
- Endpoint investigation
- Timeline development
- Evidence organization
- Incident reconstruction
- Technical reporting

Investigation activities will use authorized lab systems and simulated, generated, sanitized, or otherwise appropriate data.

---

## BR-21 — Intelligence and Analysis Capability

Stoneleaf Services requires the environment to progressively support intelligence collection and analytical development.

Capabilities may include:

- Open-source research
- Public-source information collection
- Source evaluation
- Information verification
- Collection planning
- Information organization
- Timeline analysis
- Link and relationship analysis
- Pattern identification
- Analytical writing
- Intelligence reporting

These capabilities will be developed progressively as appropriate knowledge, tools, procedures, and safeguards are established.

---

## BR-22 — Separation of Organizational Functions

The simulated organization should contain different functional roles so that realistic access controls and information boundaries can be created.

For example, an employee assigned to management should not automatically receive the same access as an investigator, intelligence analyst, system administrator, or security administrator.

This separation will support realistic exercises involving:

- Role-Based Access Control
- Least privilege
- Group membership
- Access reviews
- Permissions
- Insider-risk scenarios
- Authentication investigations
- Authorization failures
- Employee transfers
- Account provisioning
- Account deprovisioning

---

## BR-23 — Employee Lifecycle Management

The environment must support realistic employee lifecycle scenarios.

Stoneleaf Services must be able to simulate:

### Onboarding

- Creation of a new identity
- Account provisioning
- Department assignment
- Group membership
- Workstation access
- Resource access

### Role Changes

- Department transfers
- Promotions
- Management changes
- New responsibilities
- Access modifications
- Removal of unnecessary permissions

### Offboarding

- Account disablement
- Access revocation
- Group removal
- Administrative review
- Preservation of appropriate records

These scenarios will provide opportunities for both administrative and security exercises.

---

## BR-24 — Cloud and Hybrid Expansion

Stoneleaf Services requires the environment to support future integration with Microsoft cloud technologies.

Future requirements may include:

- Microsoft Azure
- Microsoft Entra ID
- Cloud identities
- Cloud networking
- Cloud virtual machines
- Cloud storage
- Role-Based Access Control
- Security monitoring
- Hybrid connectivity
- Hybrid identity
- Cloud security

Cloud capabilities will be introduced after the core on-premises infrastructure is functional and documented.

---

## BR-25 — Scalability

The Stoneleaf Services architecture must allow the environment to expand without requiring a complete redesign.

Future expansion may include:

- Additional servers
- Additional endpoints
- Additional network segments
- VLANs
- Additional security controls
- Centralized monitoring
- Cloud resources
- Hybrid infrastructure
- Investigation platforms
- Analytical tools
- Automation
- Additional simulated users

Expansion should occur only when supported by documented requirements.

---

## BR-26 — Resource Efficiency

Stoneleaf Services must operate within available computing and financial resources.

The environment should make efficient use of:

- CPU
- Memory
- SSD storage
- Backup storage
- Network bandwidth
- Cloud resources
- Software licensing

Not every virtual machine must operate continuously.

Systems may be started and stopped according to the requirements of individual projects, exercises, and services.

---

## BR-27 — Backup and Recovery

Stoneleaf Services requires a strategy for protecting important organizational data, configurations, and documentation.

The environment should progressively support:

- Configuration backups
- Documentation backups
- Critical data backups
- Recovery procedures
- Restore testing
- Virtual machine recovery concepts
- Protection against accidental deletion or corruption

Backup architecture will be defined during later technical design phases.

---

## BR-28 — Portfolio Development

The Stoneleaf Services environment must support the creation of professional portfolio evidence.

Portfolio materials may include:

- Architecture diagrams
- Network diagrams
- Sanitized configurations
- Deployment documentation
- Troubleshooting case studies
- Security projects
- Incident-response exercises
- Investigation exercises
- Cloud projects
- Automation projects
- Analytical products
- Lessons learned

Published material must be reviewed to ensure sensitive information is not exposed.

---

## BR-29 — Legal, Ethical, and Authorization Boundaries

Stoneleaf Services technical, cybersecurity, investigation, and information-collection exercises must operate within applicable legal, ethical, and authorization boundaries.

Lab exercises must use:

- Owned systems
- Authorized systems
- Simulated systems
- Publicly available information where appropriate
- Generated or sanitized data where appropriate

The environment is not intended to facilitate unauthorized access, unlawful surveillance, unauthorized interception, or unauthorized collection of information.

---

## BR-30 — Progressive Capability Development

Stoneleaf Services will follow a progressive development model.

New services, technologies, and capabilities should be introduced when the underlying knowledge and infrastructure necessary to support them have been developed.

The intended general progression is:

**IT Infrastructure → Networking and Systems Administration → Cybersecurity → Digital Investigations → Intelligence Collection → Intelligence Analysis → Professional Services**

This progression is not intended to prevent overlap between areas. It provides a framework for ensuring that advanced capabilities are built on a strong technical foundation.

---

## Business Requirements Summary

The Stoneleaf Services environment must ultimately provide:

1. A realistic 40-person simulated organization.
2. Forty unique fictional employee identities.
3. Centralized identity and access management.
4. Role-based permissions and least privilege.
5. Reliable network and internet connectivity.
6. Centralized Windows administration.
7. Linux administration capability.
8. Virtualized infrastructure.
9. Security controls.
10. Logging and monitoring.
11. Systematic troubleshooting capability.
12. Change management.
13. Reproducible technical documentation.
14. Digital investigation capability.
15. Intelligence collection and analytical capability.
16. Employee lifecycle management.
17. Future Azure and Entra ID integration.
18. Backup and recovery capability.
19. Scalable infrastructure.
20. Professional portfolio development.

---

## Current Status

**Phase:** Foundation Planning and Documentation

The business requirements defined in this document will be used to determine the technical requirements and architecture of the Stoneleaf Services environment.

Requirements may be revised as the organization, home lab, technical capabilities, and long-term business direction evolve.

---

## Next Foundation Document

The next Foundation document is:

**`Technical-Requirements.md`**

The Technical Requirements document will translate these business requirements into specific infrastructure requirements.

For example:

**Business requirement:**

> Stoneleaf Services requires centralized identity management for 40 simulated employees.

**Technical requirement:**

> Deploy Windows Server with Active Directory Domain Services and create a domain structure capable of supporting 40 unique user identities, organizational units, security groups, computer accounts, and role-based access controls.

This separation ensures that Stoneleaf Services first defines **what the organization needs** before deciding exactly **how technology will provide it**.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
