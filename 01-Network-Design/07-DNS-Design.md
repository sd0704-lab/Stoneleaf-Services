# Stoneleaf Services — DNS Design

**No Stone Left Unturned**

## Purpose

This document defines the planned Domain Name System (DNS) architecture for Stoneleaf Services.

It builds on `05-VLAN-and-Virtual-Network-Design.md` and `06-DHCP-Design.md` and establishes internal name resolution, Active Directory dependencies, external forwarding, record management, security boundaries, recovery requirements, and validation criteria.

All configurations remain **planned** until implemented and validated. Namespace and forwarding decisions identified as pending must be resolved before deployment.

---

# Design Objectives

The DNS design must:

1. Support Active Directory discovery, authentication, and Group Policy.
2. Provide consistent internal and external name resolution.
3. Preserve Infrastructure, User Endpoint, Management, and Testing boundaries.
4. Supply domain clients with the correct internal DNS service.
5. Support secure registration and controlled administration.
6. Provide documented troubleshooting and recovery procedures.
7. Support future Azure integration.
8. Distinguish design approval from deployment and successful validation.

---

# Primary DNS Architecture

## Internal DNS Server

| Setting | Planned Value |
|---|---|
| Hostname | `SLS-DC01` |
| Platform | Windows Server |
| Roles | Active Directory Domain Services and DNS |
| VMware network | `VMnet2` |
| Network | `10.10.10.0/24` |
| Static IP address | `10.10.10.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.10.10.1` |
| Function | Authoritative internal DNS and recursive resolution for approved clients |

The initial environment contains one domain controller and one internal DNS server.

DNS redundancy is not provided during the initial deployment.

## pfSense Responsibilities

`SLS-FW01` provides routing, firewall enforcement, NAT, and approved internal DHCP services.

pfSense will distribute `10.10.10.10` to User Endpoint DHCP clients.

pfSense is not the authoritative DNS server for the Active Directory domain.

A separate pfSense resolver may later serve isolated Testing clients, subject to documented configuration and firewall review.

---

# DNS Namespace

## Required Decision

The final Active Directory DNS namespace has not been established.

Do not promote the domain controller or configure the production DHCP domain suffix until the namespace is documented.

## Namespace Requirements

The selected namespace should:

- Prefer a dedicated subdomain of a public domain controlled by the project owner.
- Avoid single-label domain names.
- Avoid conflicts with existing networks or namespaces.
- Avoid `.local`, which has multicast DNS implications.
- Support future internal and cloud integration.
- Keep private Active Directory records separate from public DNS.

This document does not establish ownership of a public domain.

## Namespace Decision Record

| Item | Current State |
|---|---|
| Controlled public parent domain, if used | Not recorded |
| Active Directory DNS namespace | Pending |
| NetBIOS domain name | Pending |
| Optional alternate user sign-in suffix | Pending |
| Public DNS provider, if applicable | Pending |

The AD DNS namespace, NetBIOS name, and optional user sign-in suffix are separate decisions.

Descriptive placeholders must not be entered as actual configuration values.

---

# Network Alignment

| VMware Network | Function | Subnet | Gateway |
|---|---|---|---|
| `VMnet8` | WAN / VMware NAT | VMware-assigned | VMware NAT gateway |
| `VMnet2` | Infrastructure | `10.10.10.0/24` | `10.10.10.1` |
| `VMnet3` | User Endpoints | `10.10.20.0/24` | `10.10.20.1` |
| `VMnet4` | Management | `10.10.30.0/24` | `10.10.30.1` |
| `VMnet5` | Lab / Testing | `10.10.60.0/24` | `10.10.60.1` |

`SLS-FW01` retains five virtual network adapters.

DNS implementation does not require additional adapters, active networks, or VLAN interfaces.

All routed cross-network DNS traffic must traverse pfSense.

Traffic between systems on the same VMware segment does not traverse pfSense and requires applicable endpoint controls.

---

# Client DNS Configuration

| System | VMware Network | IP Configuration | DNS Server |
|---|---|---|---|
| `SLS-DC01` | `VMnet2` | Static `10.10.10.10` | Its own static address after DNS installation |
| `SLS-LNX01` | `VMnet2` | Static `10.10.10.20` | `10.10.10.10` |
| `SLS-WS01` | `VMnet3` | DHCP | `10.10.10.10` through DHCP |
| `SLS-WS02` | `VMnet3` | DHCP | `10.10.10.10` through DHCP |
| `SLS-WS03` | `VMnet4` exclusively | Static `10.10.30.10` | Static `10.10.10.10` |
| Temporary Testing systems | `VMnet5` | Defined per test | Approved Testing resolver |

## Domain Controller Settings

After DNS installation, `SLS-DC01` will use:

`10.10.10.10`

Record any temporary installation resolver and replace it with the final internal configuration.

Do not leave an external DNS server configured as an alternate resolver on the promoted domain controller.

## Management Workstation Settings

`SLS-WS03` retains:

- Address: `10.10.30.10`
- Mask: `255.255.255.0`
- Gateway: `10.10.30.1`
- DNS: `10.10.10.10`
- Network: `VMnet4` exclusively

## Alternate DNS Policy

Domain members must not use public DNS, VMware NAT DNS, or pfSense as alternate DNS servers.

Alternate resolvers may be queried independently of the intended internal resolution path and can produce inconsistent Active Directory discovery.

Do not configure an unbuilt secondary DNS server.

---

# Forward Lookup Zones

## Active Directory Domain Zone

The approved AD namespace will use an AD-integrated forward lookup zone.

Dynamic updates will be configured as:

**Secure only**

Implementation documentation must record:

- Exact zone name
- AD integration
- Replication scope
- SOA record
- Name server records
- Update permissions
- Administrative permissions

## Active Directory Locator Records

Preserve and validate the `_msdcs` structure and service records created by domain deployment.

Where deployment creates a separate forest-wide `_msdcs` zone, document its name and replication scope.

Do not manually replace generated AD locator records without a documented troubleshooting procedure.

## Initial Host Records

| Hostname | Planned Address | Registration Method |
|---|---|---|
| `SLS-DC01` | `10.10.10.10` | Windows and AD registration |
| `SLS-LNX01` | `10.10.10.20` | Administrator-created record initially |
| `SLS-WS01` | DHCP-assigned | Secure Windows client registration |
| `SLS-WS02` | DHCP-assigned | Secure Windows client registration |
| `SLS-WS03` | `10.10.30.10` | Secure Windows client registration |

Fully qualified names depend on the final namespace.

Do not populate records for systems that have not been deployed.

Any pfSense management hostname must resolve to an explicitly documented management address. Do not register every firewall interface under one management name.

---

# Reverse Lookup Zones

Plan the following initial IPv4 reverse zones:

| Network | Reverse Zone |
|---|---|
| Infrastructure `10.10.10.0/24` | `10.10.10.in-addr.arpa` |
| User Endpoints `10.10.20.0/24` | `20.10.10.in-addr.arpa` |
| Management `10.10.30.0/24` | `30.10.10.in-addr.arpa` |

Use AD integration and secure updates. Record replication scope during implementation.

Administrators will maintain required PTR records initially unless client PTR registration is explicitly configured and validated.

Do not assume pfSense leases automatically create Windows DNS PTR records.

The Testing reverse zone:

`60.10.10.in-addr.arpa`

remains optional and requires a documented requirement.

---

# DHCP and Dynamic Registration

pfSense supplies User Endpoint leases and the internal DNS server address.

Windows DNS hosts the AD-integrated zones.

DHCP service ownership does not establish automatic synchronization with Windows DNS.

Domain-joined Windows clients will use their supported secure registration process. Validate the actual DHCP exchange, client policy, record ownership, and forward registration behavior.

PTR registration must be tested separately.

Linux will initially use administrator-maintained A and PTR records. Authenticated Linux dynamic updates require a separate configuration decision.

Review records when systems are renamed, rebuilt, removed, or assigned different addresses. DHCP lease expiry does not by itself establish DNS record removal.

---

# External Name Resolution

## Planned Query Path

**Approved Client → SLS-DC01 → Approved External Forwarder → pfSense NAT → VMware NAT → Internet**

Queries for authoritative internal zones are answered locally.

External queries are forwarded to approved upstream resolvers.

## Forwarder Selection

The provider and exact forwarder addresses remain pending.

Before deployment, document:

- Provider
- Resolver addresses
- Access requirements
- Availability expectations
- Privacy and logging considerations
- Firewall destinations

Do not copy temporary installer resolver settings into the final configuration without review.

## Fallback Policy

The planned design uses explicit forwarders with root-hint fallback disabled.

Verify the corresponding setting on the installed Windows Server version.

If approved forwarders fail, external resolution should fail in the documented manner rather than silently using an unauthorized upstream path.

## Forwarding Loops

Do not configure Windows DNS to forward to pfSense while pfSense forwards those same queries back to Windows DNS.

Any future conditional forwarding must identify the exact namespace, destination, and direction.

## Public Exposure

No inbound DNS port forwarding or publicly accessible recursive service is authorized.

Public DNS hosting remains separate from private Active Directory DNS.

---

# DNS Suffix Policy

Domain membership and DHCP configuration must use the approved AD namespace consistently.

Configure the DHCP domain option only after the namespace decision is complete.

Document any additional search-list policy separately.

Use fully qualified names during validation. Successful short-name resolution alone does not prove that authoritative DNS is functioning correctly.

Do not use hosts-file entries, LLMNR, NetBIOS resolution, or multicast DNS as substitutes for working AD DNS.

Endpoint and browser encrypted-DNS settings must preserve required internal resolution.

---

# Lab / Testing DNS

Testing access to Infrastructure and Management is denied by default.

Do not automatically distribute `10.10.10.10` to isolated Testing systems.

Before activating Testing DNS, document:

- Approved resolver
- Listening interfaces
- Permitted clients
- External resolution requirements
- Internal namespace restrictions
- Firewall rules
- Logging
- Internet restrictions

If pfSense Resolver is selected, validate its access controls and upstream behavior.

A domain-connected test requires an explicit exception and review of associated AD traffic. DNS access alone does not provide complete domain connectivity.

---

# Firewall Requirements

| Source | Destination | Purpose | Planned Policy |
|---|---|---|---|
| User Endpoints | `10.10.10.10` | DNS | Allow required UDP/TCP 53 |
| `SLS-WS03` | `10.10.10.10` | DNS | Allow required UDP/TCP 53 |
| Approved Infrastructure clients | `10.10.10.10` | DNS | Apply server and endpoint restrictions |
| `SLS-DC01` | Approved forwarders | External DNS | Allow required UDP/TCP 53 to specified addresses |
| Testing | Infrastructure DNS | Internal resolution | Deny by default |
| WAN | Internal DNS | Unsolicited inbound DNS | Deny |
| Domain clients | External resolvers | Direct DNS bypass | Deny under approved egress policy |
| `SLS-WS03` | `SLS-DC01` | Administration | Allow approved administrative services |

TCP 53 must not be omitted merely because many queries use UDP.

DNS permission does not replace the additional rules required for AD authentication, domain joining, Group Policy, or DNS administration.

Windows Firewall must enforce applicable restrictions for same-segment Infrastructure traffic.

Detailed rules belong in:

`09-Firewall-Policy-Matrix.md`

Traffic relationships belong in:

`10-Network-Traffic-Flow-Matrix.md`

---

# Security Requirements

1. Restrict DNS administration to authorized identities.
2. Perform privileged administration from `SLS-WS03`.
3. Use secure dynamic updates for AD-integrated zones.
4. Restrict recursive service exposure to approved networks.
5. Disable zone transfers initially.
6. Authorize specific transfer destinations only if later required.
7. Keep private records out of public DNS.
8. Review unexpected records and permission changes.
9. Protect configuration and recovery evidence.
10. Maintain server updates and relevant logging.

VMware application and console administration remain on the physical host.

DNSSEC and additional DNS security technologies are future decisions and are not claimed as implemented capabilities.

---

# Aging and Scavenging

Automatic scavenging will remain disabled during initial deployment until registration behavior, timestamps, and ownership are validated.

Before enabling it, document:

- Eligible zones
- No-refresh interval
- Refresh interval
- Server schedule
- Relationship to DHCP leases
- Static record treatment
- Recovery procedure

Perform documented manual stale-record reviews initially.

Review both A and PTR records when retiring or rebuilding systems.

---

# Availability and Recovery

The initial single DNS server is a dependency for internal name resolution and AD discovery.

Cached responses do not establish full service availability during an outage.

Use a documented AD-aware backup and recovery method, including appropriate system state protection.

Preserve:

- DNS configuration
- Zone integration and scopes
- Forwarders
- Permissions
- Static records
- Network settings
- Recovery procedures

A zone export alone is not a complete domain controller recovery plan.

Do not rely on VM snapshot reversion as the sole AD recovery method.

Recovery must include post-restore DNS and AD health checks.

---

# Monitoring and Troubleshooting

| Symptom | Initial Checks |
|---|---|
| Internal names fail | Client resolver, records, DNS service, firewall |
| External names fail | Forwarders, upstream access, NAT, fallback setting |
| Domain join fails | Client DNS, AD locator records, AD ports, time |
| FQDN works but short name fails | Primary suffix, DHCP domain option, search list |
| Wrong address returned | Stale record, duplicate registration, cache |
| Reverse lookup fails | Reverse zone, PTR record, registration method |
| Testing cannot resolve internal names | Confirm intended isolation |
| Client bypasses internal DNS | Alternate resolvers, browser settings, encrypted DNS |

Review relevant DNS, AD, and firewall events.

Use explicit-server queries and fully qualified names to isolate failures.

Ping alone does not validate DNS or AD service discovery.

---

# Future Networks and Azure

Reserved networks remain inactive:

| Future VLAN ID | Function | Subnet |
|---|---|---|
| 40 | Security Operations | `10.10.40.0/24` |
| 50 | Investigations | `10.10.50.0/24` |
| 70 | Storage / Backup | `10.10.70.0/24` |
| 80 | Network Infrastructure | `10.10.80.0/24` |

Do not populate fictional records or enable access for undeployed systems.

On-premises address space:

`10.10.0.0/16`

Reserved Azure address space:

`10.20.0.0/16`

Future hybrid DNS may require private zones, conditional forwarding, reachable resolver endpoints, VPN routing, and separate identity decisions.

Do not assume Microsoft Entra integration supplies traditional AD DNS or that Azure-provided resolution is directly reachable from on-premises systems.

---

# Implementation Dependencies

Before deployment:

- Finalize the AD DNS namespace and NetBIOS name.
- Confirm domain ownership where applicable.
- Confirm Windows Server version.
- Configure static `SLS-DC01` addressing.
- Select exact upstream forwarders.
- Complete DNS and AD firewall requirements.
- Configure DHCP DNS and suffix options.
- Define forward and reverse registration ownership.
- Establish backup and console recovery procedures.
- Approve Testing DNS before activation.

---

# Implementation Documentation

The playbook must include:

1. Prerequisites and software versions.
2. Domain promotion procedure.
3. Exact zone names and settings.
4. Replication scopes.
5. Forwarder and fallback configuration.
6. Initial records and permissions.
7. Client and DHCP settings.
8. Firewall configuration.
9. Verification steps and expected results.
10. Evidence, troubleshooting, recovery, and change records.

This design defines intended behavior. Deployment records establish what was configured.

---

# Validation Requirements

All tests remain **Not Tested**.

Record expected and actual results, date, configuration version, evidence, and pass/fail status in:

`12-Network-Validation-and-Test-Plan.md`

| Test | Expected Result |
|---|---|
| Inspect DC addressing | Correct static address, gateway, and internal resolver |
| Inspect clients | User DHCP and Management static DNS settings correct |
| Inspect zones | Approved namespace, AD integration, secure updates |
| Query SOA, NS, and A records | Correct authoritative responses |
| Query AD locator records | Correct domain controller discovery |
| Query required PTR records | Correct reverse resolution |
| Register domain client | Secure forward registration succeeds |
| Validate PTR workflow | Documented maintenance method succeeds |
| Resolve external names | Approved forwarding path works |
| Test UDP and TCP DNS | Both required transports work |
| Join domain and apply policy | Required AD behavior succeeds |
| Attempt unauthorized zone transfer | Denied |
| Query internal DNS from Testing | Blocked unless approved |
| Attempt direct external DNS | Blocked under approved policy |
| Inspect forwarding relationships | No loops |
| Test upstream failure | Documented failure without unauthorized fallback |
| Review logs | Relevant faults identifiable |
| Validate recovery procedure | Documented acceptance criteria met |

Optional tests may be marked Not Applicable only with a recorded reason.

Disruptive outage and recovery tests require a documented recovery path.

---

# Change Management

Review changes to:

- Namespaces and zones
- Replication scopes
- Forwarders and fallback
- Client resolver settings
- DHCP suffixes
- Dynamic registration
- Scavenging
- Record permissions
- Firewall access
- Hybrid forwarding

Record TTL and caching implications.

An AD domain rename requires separate impact review; it is not a routine DNS record change.

Update affected designs, playbooks, diagrams, and validation records together.

---

# Design Decisions

## DD-DNS-001 — Internal Authority

**Decision:** Use `SLS-DC01` at `10.10.10.10` for internal AD DNS.

**Reason:** Aligns DNS with the approved Infrastructure architecture.

**Status:** Planned — Pending Implementation

## DD-DNS-002 — Client Resolver Policy

**Decision:** Use internal Windows DNS for domain clients without public alternate resolvers.

**Reason:** Preserves consistent AD discovery and internal resolution.

**Status:** Planned — Pending Validation

## DD-DNS-003 — Namespace

**Decision:** Finalize the namespace before domain deployment, preferably under an owner-controlled public domain.

**Reason:** Reduces conflicts and supports future integration.

**Status:** Pending Namespace Selection

## DD-DNS-004 — External Resolution

**Decision:** Use approved explicit forwarders without root-hint fallback.

**Reason:** Establishes a defined upstream path.

**Status:** Pending Provider Selection and Version Verification

## DD-DNS-005 — Testing Isolation

**Decision:** Deny Testing access to internal DNS by default.

**Reason:** Preserves the approved security boundary.

**Status:** Planned — Pending Optional Testing Design

---

# Completion Criteria

The design is ready for implementation when:

- Namespace decisions are complete.
- Forwarders are selected.
- Zone settings are documented.
- Client and DHCP configuration is defined.
- Registration responsibilities are established.
- Firewall requirements are complete.
- Recovery procedures are available.
- Validation criteria are documented.

Implementation completion requires deployment evidence.

Validation acceptance requires successful recorded tests.

---

# Document Status

**Project:** Stoneleaf Services

**Document:** 07 — DNS Design

**Phase:** Network Design

**Status:** Planned — Pending Namespace and Forwarder Decisions

**Implementation Status:** Not Started

**Validation Status:** Not Tested

**Previous Document:** `06-DHCP-Design.md`

**Next Document:** `08-Routing-and-NAT-Design.md`
