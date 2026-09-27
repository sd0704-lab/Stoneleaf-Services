# Stoneleaf Services — Change Management

**No Stone Left Unturned**

## Purpose

This document establishes the change-management process for the Stoneleaf Services technical environment.

Change management provides a structured method for planning, documenting, implementing, validating, reviewing, and, when necessary, reversing changes to Stoneleaf Services systems.

The objective is not to create unnecessary administrative overhead.

The objective is to ensure significant technical changes are:

- Intentional
- Documented
- Understandable
- Reproducible
- Secure
- Tested
- Validated
- Recoverable
- Traceable

Change management also creates a historical record that can support troubleshooting, incident response, security analysis, system recovery, and future technical decision-making.

---

# Change Management Philosophy

Stoneleaf Services follows the principle:

**Plan → Document → Implement → Validate → Record**

Changes should not be made without understanding:

- What is changing
- Why it is changing
- What systems may be affected
- What the expected result is
- What could go wrong
- How success will be verified
- How the previous state can be restored when appropriate

The level of documentation should be proportional to the significance and risk of the change.

---

# Scope

The change-management process applies to significant changes involving:

- Network infrastructure
- VMware
- Virtual machines
- pfSense
- Routing
- DHCP
- DNS
- NAT
- Firewall rules
- Windows Server
- Active Directory
- Group Policy
- Windows workstations
- Linux systems
- User and group architecture
- Authentication
- Authorization
- Security controls
- Logging
- Monitoring
- Storage
- Backup and recovery
- Cloud infrastructure
- Microsoft Azure
- Microsoft Entra ID
- Investigation systems
- Analytical systems
- Important software
- Important configuration
- Architecture
- Documentation affecting technical operations

Not every minor action requires a formal change record.

---

# Change Identifier Standard

Formal Stoneleaf Services changes will use:

`CHG-YYYY-###`

Example:

`CHG-2027-001`

Where:

- `CHG` = Change
- `YYYY` = Year
- `###` = Sequential change number

Examples:

- `CHG-2027-001`
- `CHG-2027-002`
- `CHG-2027-003`

Change identifiers must not be reused.

---

# Change Title Standard

Each change should have a short descriptive title.

Example:

`CHG-2027-001 — Deploy SLS-DC01`

Another example:

`CHG-2027-002 — Modify SLS-FW01 DHCP Configuration`

Titles should describe the primary action being performed.

---

# Change Categories

Stoneleaf Services changes may be classified into the following categories.

## Standard Change

A Standard Change is a routine, understood, repeatable, and relatively low-risk change.

Examples may include:

- Approved software installation
- Routine system update
- Creating a documented user account
- Adding a user to an approved group
- Repeating a previously validated configuration procedure

A Standard Change may require less documentation than a significant infrastructure change.

---

## Normal Change

A Normal Change is a planned change requiring evaluation before implementation.

Examples include:

- Deploying a new server
- Modifying network configuration
- Changing DHCP settings
- Modifying DNS
- Creating a new Group Policy Object
- Changing firewall rules
- Changing access-control architecture
- Deploying a new security tool
- Adding a new network segment

Most significant Stoneleaf Services infrastructure changes will initially fall into this category.

---

## Emergency Change

An Emergency Change is performed when immediate action is required to:

- Restore critical functionality
- Contain a security incident
- Correct a serious configuration failure
- Prevent significant data loss
- Address an urgent security problem

Emergency changes may be implemented before complete documentation is created when delay would create greater risk.

The change must be documented as soon as practical afterward.

---

# Change Significance

Changes should also be evaluated according to their potential impact.

## Low Impact

A Low Impact change:

- Affects a limited component
- Has a predictable outcome
- Is easily reversible
- Has little effect on other systems

## Moderate Impact

A Moderate Impact change:

- May affect multiple components
- Has dependencies
- Could temporarily affect services
- Requires meaningful validation

## High Impact

A High Impact change:

- Affects critical infrastructure
- Could affect multiple systems or users
- Could affect authentication or connectivity
- Could create significant security implications
- May be difficult to reverse
- Could result in data loss or extended service interruption

Impact classification should help determine how much planning and validation is appropriate.

---

# Change Risk Assessment

Before implementing a significant change, the following should be considered:

- Systems affected
- Users affected
- Services affected
- Dependencies
- Security implications
- Availability impact
- Data-loss potential
- Authentication impact
- Network impact
- Recovery difficulty
- Rollback capability
- Required downtime
- Required storage
- Required resources

Risk assessment does not need to become unnecessarily complex for simple lab changes.

The purpose is to identify likely consequences before making the change.

---

# Change Record Requirements

A formal change record should include where applicable:

1. Change ID
2. Change title
3. Date
4. Change category
5. Impact level
6. Requestor
7. Purpose
8. Reason for change
9. Systems affected
10. Dependencies
11. Current configuration
12. Proposed configuration
13. Security considerations
14. Risk assessment
15. Prerequisites
16. Backup requirements
17. Implementation plan
18. Validation plan
19. Rollback plan
20. Actual implementation
21. Validation results
22. Problems encountered
23. Final configuration
24. Final status
25. Related documentation
26. Lessons learned

Not every change requires every field.

Documentation should remain proportional to the complexity and risk of the change.

---

# Change Lifecycle

Stoneleaf Services changes should generally follow this lifecycle:

```text
Identify Need
     ↓
Create Change Record
     ↓
Evaluate Impact and Risk
     ↓
Identify Dependencies
     ↓
Create Implementation Plan
     ↓
Create Validation Plan
     ↓
Create Rollback Plan
     ↓
Prepare Backups if Required
     ↓
Implement Change
     ↓
Validate Change
     ↓
Troubleshoot if Required
     ↓
Document Final Configuration
     ↓
Update Related Documentation
     ↓
Close Change
