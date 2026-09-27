# Stoneleaf Services — Naming Standards

**No Stone Left Unturned**

## Purpose

This document establishes standardized naming conventions for Stoneleaf Services technical resources.

Consistent naming improves:

- Administration
- Troubleshooting
- Security
- Documentation
- Automation
- Asset identification
- Access management
- Incident response
- Digital investigations
- Cloud administration
- Scalability

Naming standards should make resources understandable without requiring unnecessary additional investigation.

These standards apply to the Stoneleaf Services lab environment and may evolve as the organization and technical infrastructure develop.

---

# General Naming Principles

Stoneleaf Services naming conventions should follow these principles:

1. Names must be consistent.
2. Names should communicate the purpose of the resource.
3. Names should remain reasonably short.
4. Names should avoid unnecessary complexity.
5. Names should support future expansion.
6. Names should avoid sensitive information.
7. Names should be unique within the appropriate namespace.
8. Names should use predictable abbreviations.
9. Naming should support troubleshooting and automation.
10. Existing naming standards should be followed before creating new naming patterns.

---

# Organization Identifier

The standard Stoneleaf Services abbreviation is:

`SLS`

This identifier will be used where an organizational prefix improves clarity.

Examples:

- `SLS-FW01`
- `SLS-DC01`
- `SLS-LNX01`
- `SLS-WS01`

The organization should be written as:

**Stoneleaf Services**

The standard motto is:

**No Stone Left Unturned**

---

# Computer Naming Standard

Stoneleaf Services computer names will generally use the following format:

`SLS-[ROLE][NUMBER]`

Example:

`SLS-DC01`

Where:

- `SLS` = Stoneleaf Services
- `DC` = Domain Controller
- `01` = Sequential system number

---

# Approved System Role Codes

| Code | Meaning | Example |
| --- | --- | --- |
| `FW` | Firewall / Router | `SLS-FW01` |
| `DC` | Domain Controller | `SLS-DC01` |
| `LNX` | Linux Server | `SLS-LNX01` |
| `WS` | Windows Workstation | `SLS-WS01` |
| `FS` | File Server | `SLS-FS01` |
| `WEB` | Web Server | `SLS-WEB01` |
| `DB` | Database Server | `SLS-DB01` |
| `LOG` | Logging Server | `SLS-LOG01` |
| `MON` | Monitoring Server | `SLS-MON01` |
| `SEC` | Security System | `SLS-SEC01` |
| `BK` | Backup System | `SLS-BK01` |
| `NAS` | Network-Attached Storage | `SLS-NAS01` |
| `TEST` | Testing System | `SLS-TEST01` |

New role codes may be introduced when a documented requirement exists.

---

# Initial System Names

The initial permanent Stoneleaf Services systems are:

| Hostname | Function |
| --- | --- |
| `SLS-FW01` | Firewall / Router |
| `SLS-DC01` | Domain Controller / DNS |
| `SLS-LNX01` | Linux Server |
| `SLS-WS01` | Investigations Workstation |
| `SLS-WS02` | Intelligence and Analysis Workstation |
| `SLS-WS03` | Management and Administrative Workstation |

These names establish the initial system-naming baseline.

---

# Sequential Numbering

Sequential numbers should normally use two digits.

Examples:

`01`

`02`

`03`

This allows systems to be added without changing the naming format.

Examples:

`SLS-DC01`

`SLS-DC02`

`SLS-LNX01`

`SLS-LNX02`

`SLS-WS01`

`SLS-WS02`

---

# Employee Identity Standard

Stoneleaf Services will simulate **40 individual employees**.

Every employee must have a unique fictional identity.

Generic primary identities such as:

`user01`

`employee01`

`testuser01`

should not be used for the simulated workforce.

Each employee record should include:

- Employee ID
- First name
- Last name
- Job title
- Department
- Manager
- Username
- User Principal Name
- Email address
- Organizational Unit
- Security-group memberships
- Privilege classification
- Assigned resources where applicable

All simulated identities must be fictional.

---

# Employee ID Standard

Employee IDs will use the following format:

`SLS-####`

Example:

`SLS-1001`

The initial simulated workforce should begin with:

`SLS-1001`

and continue sequentially.

Examples:

- `SLS-1001`
- `SLS-1002`
- `SLS-1003`
- `SLS-1004`

The employee ID must remain associated with the fictional employee even if that employee changes departments, positions, or managers.

Employee IDs should not be reused.

---

# Standard Username Format

Standard employee usernames will use:

`first.last`

Example:

Employee:

**Daniel Mercer**

Username:

`daniel.mercer`

This format provides clear identity attribution during:

- Administration
- Logging
- Troubleshooting
- Security monitoring
- Incident response
- Digital investigations

If duplicate names occur, an approved differentiation method must be documented before creating the account.

---

# User Principal Name Standard

The User Principal Name format will be:

`first.last@[DOMAIN]`

Example format:

`daniel.mercer@[DOMAIN]`

The actual Stoneleaf Services domain namespace has not yet been selected.

The domain portion must therefore remain a design decision until the Active Directory namespace is formally established.

Once selected, the same standard should be applied consistently to all employee identities.

---

# Email Address Standard

The standard organizational email format will be:

`first.last@[EMAIL-DOMAIN]`

Example:

`daniel.mercer@[EMAIL-DOMAIN]`

The final organizational email domain will be determined when the appropriate domain and cloud architecture are established.

Email addresses documented before that decision should use placeholders rather than assuming a production domain.

---

# Display Name Standard

Employee display names should use:

`First Last`

Example:

`Daniel Mercer`

Job titles, departments, employee IDs, and other attributes should be stored in their appropriate directory fields rather than unnecessarily embedded into the display name.

---

# Administrative Account Standard

Privileged administrative activity should use accounts separate from normal employee identities where practical.

Administrative accounts will use:

`adm-first.last`

Example:

Standard account:

`daniel.mercer`

Administrative account:

`adm-daniel.mercer`

This allows administrative activity to be distinguished from ordinary user activity in logs and investigations.

Administrative accounts must not be created for users who do not require elevated access.

---

# Service Account Standard

Service accounts will use:

`svc-[function]`

Examples:

`svc-backup`

`svc-monitoring`

`svc-logging`

Service accounts must:

- Have a documented purpose
- Have a documented owner
- Receive only required permissions
- Not be used as normal employee accounts
- Be reviewed periodically
- Be disabled when no longer required

Passwords, secrets, and credentials associated with service accounts must not be stored in public documentation.

---

# Test Account Standard

Accounts specifically created for temporary testing should use:

`test-[purpose]`

Examples:

`test-dns`

`test-gpo`

`test-auth`

Temporary test accounts should be removed or disabled when the associated exercise is complete unless a documented requirement exists to retain them.

---

# Group Naming Standards

Active Directory groups must use consistent prefixes identifying their purpose.

The following initial group categories will be used.

---

## Security Groups

General security groups will use:

`SG-[FUNCTION]`

Examples:

`SG-IT`

`SG-Security`

`SG-Investigations`

`SG-Intelligence`

---

## Department Groups

Department-based groups will use:

`SG-DEPT-[DEPARTMENT]`

Examples:

`SG-DEPT-IT`

`SG-DEPT-Security`

`SG-DEPT-Investigations`

`SG-DEPT-Intelligence`

---

## Role Groups

Role-based groups will use:

`SG-ROLE-[ROLE]`

Examples:

`SG-ROLE-Managers`

`SG-ROLE-Investigators`

`SG-ROLE-Analysts`

`SG-ROLE-Administrators`

---

## Resource Access Groups

Groups controlling access to specific resources should use:

`SG-RES-[RESOURCE]-[ACCESS]`

Examples:

`SG-RES-Investigations-R`

`SG-RES-Investigations-RW`

`SG-RES-Intelligence-R`

`SG-RES-Intelligence-RW`

Where:

- `R` = Read
- `RW` = Read / Write

Additional permission identifiers may be defined when required.

---

# Group Naming Principle

Group names should identify **why the group exists**.

Permissions should be assigned to groups rather than directly to individual users whenever practical.

This allows access to follow organizational roles instead of requiring individual permission management.

---

# Organizational Unit Naming

Organizational Units should use clear descriptive names.

Examples may include:

`Users`

`Workstations`

`Servers`

`Administrative Accounts`

`Service Accounts`

The final OU structure will be determined during Active Directory design.

OU structure should primarily support:

- Administration
- Group Policy
- Delegation
- Security

The OU structure should not automatically duplicate the organizational chart.

---

# Department Naming

Department names must be standardized before the 40 fictional employee identities are created.

Once a department name is established, the same terminology should be used across:

- Active Directory
- Employee records
- Security groups
- Documentation
- Access-control records
- Incident reports
- Investigation records
- Cloud identities

Abbreviations should not vary between systems without a documented reason.

The final department structure will be established during organizational and identity design.

---

# Network Object Naming

Network infrastructure should use descriptive standardized names.

Examples:

`SLS-FW01`

`SLS-SW01`

`SLS-AP01`

Where appropriate:

- `FW` = Firewall
- `SW` = Switch
- `AP` = Wireless Access Point

Additional network naming standards may be established during network design.

---

# Network Naming and VLANs

If VLANs are introduced, they must use documented names that describe their function.

Potential naming examples include:

`VLAN-Users`

`VLAN-Servers`

`VLAN-Management`

`VLAN-Security`

VLAN IDs, names, and subnet assignments will be determined during network design.

The naming standard does not require VLAN deployment.

---

# DNS Hostnames

DNS host records should correspond to standardized system hostnames wherever practical.

Example:

Hostname:

`SLS-DC01`

DNS hostname format:

`SLS-DC01.[DOMAIN]`

The domain namespace will be determined during Active Directory and network design.

Aliases may be used when a service-oriented DNS name improves administration or usability.

---

# VMware Naming

Virtual machine names should normally match the hostname of the operating system.

Example:

VMware VM name:

`SLS-DC01`

Windows hostname:

`SLS-DC01`

This reduces confusion between:

- VMware
- Operating systems
- Network documentation
- Logs
- Troubleshooting records

Temporary VM names may include additional descriptive information when necessary.

---

# Snapshot Naming

VMware snapshots should use descriptive names.

Recommended format:

`YYYY-MM-DD-[DESCRIPTION]`

Examples:

`2027-01-15-Before-ADDS`

`2027-01-16-Before-GPO-Test`

`2027-01-20-Before-DNS-Change`

Snapshot names should indicate why the snapshot was created.

Snapshots should not be treated as permanent backups.

---

# Hardware Asset Naming

Physical hardware will use:

`HW-###`

Examples:

`HW-001`

`HW-002`

`HW-003`

Hardware asset identifiers must remain associated with the physical asset throughout its Stoneleaf Services lifecycle.

---

# Software Asset Naming

Software inventory entries will use:

`SW-###`

Examples:

`SW-001`

`SW-002`

`SW-003`

Software identifiers provide consistent references across technical documentation.

---

# Cloud Resource Naming

Microsoft Azure and other cloud resources will require standardized naming.

The exact Azure naming convention will be established during cloud architecture design because Azure resource types have different naming restrictions.

Cloud naming should communicate attributes such as:

- Organization
- Resource type
- Workload
- Environment
- Sequence where required

Potential conceptual format:

`[ORG]-[RESOURCE]-[FUNCTION]-[NUMBER]`

Example:

`SLS-VM-DC-01`

This is a conceptual example and does not establish the final Azure naming convention.

---

# Environment Identification

If Stoneleaf Services later introduces separate environments, standard environment identifiers should be used.

Potential identifiers include:

| Code | Environment |
| --- | --- |
| `PROD` | Production |
| `LAB` | Laboratory |
| `TEST` | Testing |
| `DEV` | Development |

Environment identifiers should only be introduced when multiple environments actually exist and distinguishing between them provides operational value.

---

# Documentation Naming

Documentation filenames should clearly identify their contents.

Preferred format:

`Descriptive-Document-Name.md`

Examples:

`Business-Requirements.md`

`Technical-Requirements.md`

`Hardware-Inventory.md`

`Software-Inventory.md`

`Naming-Standards.md`

`Documentation-Standards.md`

Words should generally be separated using hyphens.

---

# Directory Naming

Major GitHub directories will use numerical prefixes to preserve logical project order.

Current structure:

`00-Foundation`

`01-Network-Design`

`02-VMware`

`03-pfSense`

`04-Windows-Server`

`05-Windows-Clients`

`06-Linux`

`07-Security`

`08-Logging-Monitoring`

`09-Troubleshooting-Labs`

`10-Incident-Reports`

`11-Azure-Entra`

`12-Projects`

Supporting directories may include:

`diagrams`

`templates`

`assets`

`screenshots`

---

# Troubleshooting Lab Naming

Troubleshooting exercises should receive unique identifiers.

Recommended format:

`TS-###`

Examples:

`TS-001`

`TS-002`

`TS-003`

A descriptive title should accompany the identifier.

Example:

`TS-001 — Client Cannot Reach Default Gateway`

---

# Incident Naming

Simulated security incidents should receive unique identifiers.

Recommended format:

`INC-YYYY-###`

Example:

`INC-2027-001`

A descriptive incident title should accompany the identifier.

Example:

`INC-2027-001 — Repeated Failed Authentication Attempts`

---

# Investigation Naming

Formal simulated investigations should receive unique identifiers.

Recommended format:

`INV-YYYY-###`

Example:

`INV-2027-001`

A descriptive title should accompany the identifier.

Investigation identifiers allow evidence, timelines, reports, screenshots, and related artifacts to be associated with the same case.

---

# Change Record Naming

Change records will use:

`CHG-YYYY-###`

Example:

`CHG-2027-001`

A descriptive title should accompany the identifier.

Example:

`CHG-2027-001 — Deploy SLS-DC01`

---

# Project Naming

Formal Stoneleaf Services projects should receive unique identifiers.

Recommended format:

`PRJ-YYYY-###`

Example:

`PRJ-2027-001`

A descriptive project name should accompany the identifier.

Example:

`PRJ-2027-001 — Active Directory Deployment`

---

# Account Naming Restrictions

User and system account names should avoid:

- Spaces where technically inappropriate
- Unnecessary special characters
- Offensive terminology
- Sensitive personal information
- Birth dates
- Social Security numbers
- Phone numbers
- Password information
- Security answers
- Unnecessary organizational secrets

Naming conventions should remain compatible with the systems in which the identities will be used.

---

# Duplicate Name Handling

If two simulated employees have the same first and last name, the collision must be resolved using a documented and consistent method.

The preferred approach is to preserve the employee's readable identity while introducing the minimum additional information necessary to create a unique username.

Potential approaches may include:

- Middle initial
- Sequential suffix

Example:

`daniel.r.mercer`

A final duplicate-name rule should be selected if an actual collision occurs.

Employee IDs will remain unique regardless of name duplication.

---

# Name Changes

If a simulated employee's name changes as part of an identity-management exercise:

- Employee ID must remain unchanged.
- Identity history should be documented.
- Username changes should follow documented procedures.
- Email changes should follow documented procedures.
- Access permissions must be reviewed.
- References in applicable identity records should be updated.

This provides an opportunity to simulate realistic identity lifecycle administration.

---

# Naming Governance

New naming patterns should not be created when an existing Stoneleaf Services standard already applies.

If a new resource type requires a naming convention:

1. Identify the resource type.
2. Determine whether an existing standard applies.
3. Define a clear naming pattern if necessary.
4. Document the new pattern.
5. Apply it consistently.
6. Update this document when appropriate.

Significant naming-standard changes should follow the Stoneleaf Services change-management process.

---

# Security Considerations

Names should provide enough information for administration without unnecessarily exposing sensitive information.

Public documentation should not include sensitive identifiers such as:

- Real personal information
- Passwords
- Authentication secrets
- Recovery information
- Private keys
- API keys
- Tokens
- Public IP addresses where disclosure is unnecessary
- Device serial numbers

The 40 simulated Stoneleaf Services employee identities must remain clearly fictional.

---

# Naming Standards Summary

| Resource | Standard | Example |
| --- | --- | --- |
| Organization | `SLS` | `SLS` |
| Computer | `SLS-[ROLE][##]` | `SLS-DC01` |
| Employee ID | `SLS-####` | `SLS-1001` |
| User Account | `first.last` | `daniel.mercer` |
| Administrative Account | `adm-first.last` | `adm-daniel.mercer` |
| Service Account | `svc-[function]` | `svc-backup` |
| Test Account | `test-[purpose]` | `test-dns` |
| Security Group | `SG-[FUNCTION]` | `SG-IT` |
| Department Group | `SG-DEPT-[DEPARTMENT]` | `SG-DEPT-IT` |
| Role Group | `SG-ROLE-[ROLE]` | `SG-ROLE-Analysts` |
| Resource Group | `SG-RES-[RESOURCE]-[ACCESS]` | `SG-RES-Investigations-RW` |
| Hardware | `HW-###` | `HW-001` |
| Software | `SW-###` | `SW-001` |
| Troubleshooting Lab | `TS-###` | `TS-001` |
| Incident | `INC-YYYY-###` | `INC-2027-001` |
| Investigation | `INV-YYYY-###` | `INV-2027-001` |
| Change | `CHG-YYYY-###` | `CHG-2027-001` |
| Project | `PRJ-YYYY-###` | `PRJ-2027-001` |
| Snapshot | `YYYY-MM-DD-[DESCRIPTION]` | `2027-01-15-Before-ADDS` |

---

# Current Status

**Standard Version:** 1.0

**Phase:** Foundation Planning and Documentation

These standards establish the initial naming framework for Stoneleaf Services.

Additional naming conventions may be introduced as new infrastructure, cloud resources, security platforms, investigation systems, and analytical capabilities are implemented.

---

# Next Foundation Document

The next Foundation document is:

**`Documentation-Standards.md`**

The Documentation Standards document will define how Stoneleaf Services creates, formats, organizes, versions, validates, and maintains technical documentation.

---

**Stoneleaf Services**  
*No Stone Left Unturned*
