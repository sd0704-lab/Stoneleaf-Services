# Stoneleaf Services — DHCP Design

**No Stone Left Unturned**

## Purpose

This document defines the planned Dynamic Host Configuration Protocol (DHCP) architecture for Stoneleaf Services.

It builds on `05-VLAN-and-Virtual-Network-Design.md` and defines DHCP service ownership, address pools, client configuration, static addressing boundaries, security requirements, implementation dependencies, and validation criteria.

All configurations remain **planned** until implementation and validation are completed. Design decisions do not establish that services are operational or tests have passed.

---

# Design Objectives

The DHCP design must:

1. Provide consistent addressing for organizational workstations.
2. Supply the correct subnet mask, default gateway, and DNS server.
3. Prevent conflicts between dynamic leases and static addresses.
4. Prevent competing VMware and pfSense DHCP services.
5. Preserve Infrastructure, User Endpoint, Management, and Testing boundaries.
6. Support Active Directory authentication and internal DNS.
7. Provide documented troubleshooting and recovery procedures.
8. Support repeatable implementation and future expansion.

---

# DHCP Service Architecture

## Internal DHCP Authority

`SLS-FW01` will provide DHCP for approved internal scopes.

VMware DHCP must be disabled on:

- `VMnet2` — Infrastructure
- `VMnet3` — User Endpoints
- `VMnet4` — Management
- `VMnet5` — Lab / Testing

Windows Server DHCP will not be deployed initially.

The installed pfSense version, DHCP backend, and supported configuration settings must be recorded in the implementation playbook.

## WAN DHCP

VMware DHCP on `VMnet8` will supply the pfSense WAN configuration.

This service is separate from internal pfSense DHCP. The requirement to disable VMware DHCP applies to the four internal VMnets, not `VMnet8`.

The actual WAN subnet, lease, gateway, and upstream settings must be recorded during implementation.

---

# Network and DHCP Assignments

| VMware Network | Function | Subnet | Gateway | Initial DHCP State |
|---|---|---|---|---|
| `VMnet8` | WAN / External | VMware-assigned | VMware NAT gateway | VMware DHCP available for pfSense WAN |
| `VMnet2` | Infrastructure | `10.10.10.0/24` | `10.10.10.1` | Disabled; static systems |
| `VMnet3` | User Endpoints | `10.10.20.0/24` | `10.10.20.1` | pfSense scope planned |
| `VMnet4` | Management | `10.10.30.0/24` | `10.10.30.1` | Disabled; static management |
| `VMnet5` | Lab / Testing | `10.10.60.0/24` | `10.10.60.1` | Disabled until testing scope approval |

All internal networks use subnet mask:

`255.255.255.0`

No DHCP relay is required initially because pfSense has a directly connected interface on each internal network.

---

# pfSense Interface Model

`SLS-FW01` will have five virtual network adapters.

| Logical Interface | VMware Network | Address | DHCP Role |
|---|---|---|---|
| WAN | `VMnet8` | VMware-assigned | DHCP client |
| LAN / Infrastructure | `VMnet2` | `10.10.10.1/24` | Server disabled |
| OPT1 / User Endpoints | `VMnet3` | `10.10.20.1/24` | DHCP server |
| OPT2 / Management | `VMnet4` | `10.10.30.1/24` | Server disabled |
| OPT3 / Lab / Testing | `VMnet5` | `10.10.60.1/24` | Optional DHCP server |

Actual adapter identifiers must be verified using VMware MAC addresses and pfSense interface information. Adapter enumeration must not be assumed.

---

# User Endpoint DHCP Scope

## Scope Configuration

| Setting | Planned Value |
|---|---|
| Network | `10.10.20.0/24` |
| VMware network | `VMnet3` |
| pfSense interface | OPT1 / User Endpoints |
| Dynamic pool start | `10.10.20.100` |
| Dynamic pool end | `10.10.20.199` |
| Pool capacity | 100 addresses |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.10.20.1` |
| DNS server | `10.10.10.10` |
| Domain / search suffix | Final Active Directory namespace |
| Proposed default lease | 8 hours |
| Proposed maximum lease | 24 hours |

Lease durations are proposed planning values. Confirm their supported settings in the selected pfSense DHCP backend before implementation.

The final domain name must be established in `07-DNS-Design.md`. Placeholder domain names must not be entered into the deployed scope.

## Initial Clients

| System | Function | Addressing |
|---|---|---|
| `SLS-WS01` | Investigations Workstation | DHCP |
| `SLS-WS02` | Intelligence / Analysis Workstation | DHCP |

`SLS-WS03` is not a member of this network. It connects exclusively to `VMnet4`.

## Address Allocation

| Address Range | Purpose |
|---|---|
| `10.10.20.0` | Network address; unavailable |
| `10.10.20.1` | pfSense gateway |
| `10.10.20.2 – 10.10.20.99` | Reserved for documented fixed assignments |
| `10.10.20.100 – 10.10.20.199` | Dynamic pool |
| `10.10.20.200 – 10.10.20.254` | Reserved for future allocation |
| `10.10.20.255` | Broadcast address; unavailable |

Reserved addresses are not active assignments. Allocations must be recorded in the IP Addressing Plan.

---

# Infrastructure Addressing

No Infrastructure DHCP scope will be active initially.

| System | Static Address | Gateway | DNS |
|---|---|---|---|
| `SLS-FW01` Infrastructure interface | `10.10.10.1/24` | Not applicable as an endpoint setting | Firewall DNS policy defined separately |
| `SLS-DC01` | `10.10.10.10/24` | `10.10.10.1` | Defined in DNS Design |
| `SLS-LNX01` | `10.10.10.20/24` | `10.10.10.1` | `10.10.10.10` |

Future Infrastructure DHCP must exclude existing static addresses and receive a documented scope review before activation.

---

# Management Addressing

## Dedicated Management Workstation

`SLS-WS03` will use manually configured static addressing.

| Setting | Required Value |
|---|---|
| VMware network | `VMnet4` exclusively |
| IP address | `10.10.30.10` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `10.10.30.1` |
| Primary DNS | `10.10.10.10` |
| Domain membership | Stoneleaf Services Active Directory |

The Management workstation must not receive an additional adapter connecting it directly to another security zone.

## Management Allocation

| Address Range | Purpose |
|---|---|
| `10.10.30.1` | pfSense Management gateway |
| `10.10.30.10` | `SLS-WS03` |
| `10.10.30.11 – 10.10.30.49` | Reserved Management systems |
| `10.10.30.50 – 10.10.30.99` | Reserved Infrastructure management |
| `10.10.30.100 – 10.10.30.199` | Reserved future DHCP pool |

No Management DHCP scope will be active initially. Other usable addresses remain unallocated until documented.

---

# Lab / Testing DHCP

The Testing network will exist even when no DHCP scope or permanent testing systems are active.

| Setting | Proposed Value |
|---|---|
| Network | `10.10.60.0/24` |
| VMware network | `VMnet5` |
| Gateway | `10.10.60.1` |
| Dynamic pool | `10.10.60.100 – 10.10.60.199` |
| Default lease | 2 hours |
| Maximum lease | 8 hours |
| Initial state | Disabled |

These pool and lease values are proposals requiring review before activation.

## Testing DNS Policy

Testing access to Infrastructure and Management is denied by default.

Do not automatically distribute `10.10.10.10` to testing clients when firewall policy prevents access to that server.

Before scope activation, document an approved reachable DNS service. If pfSense DNS Resolver is selected, configure and validate its listening interfaces, access controls, forwarding behavior, and internal namespace restrictions.

Any exception permitting testing access to internal DNS must appear in `09-Firewall-Policy-Matrix.md`.

Do not distribute the Active Directory search suffix to isolated testing clients by default.

---

# DNS and Active Directory Integration

Domain-joined User workstations will receive:

`10.10.10.10`

The same address will be configured statically on `SLS-WS03`.

Public DNS servers must not be configured as alternate DNS servers on domain-joined clients. External resolution must follow the internal DNS forwarding design.

DHCP does not:

- Join systems to Active Directory.
- Authorize access to infrastructure.
- Automatically establish Windows DNS registration.
- Replace firewall rules required for authentication and Group Policy.

Secure DNS updates, client registration, reverse records, and the final namespace will be defined in `07-DNS-Design.md`.

Do not assume pfSense leases automatically create records in Windows DNS.

---

# DHCP Options

Each active scope must supply the correct:

- Subnet mask
- Local pfSense gateway
- Approved DNS server
- Domain name or search suffix, where applicable
- Lease settings

Optional NTP, PXE, TFTP, custom routes, and other settings require documented requirements.

DHCP time settings do not replace the Active Directory time hierarchy for domain members.

This document defines IPv4 DHCP. IPv6 addressing, router advertisements, and DHCPv6 require a separate documented decision before deployment.

---

# Static Addresses and Reservations

A manually configured static address is set on the endpoint.

A DHCP reservation or static mapping supplies an intended address through DHCP.

Critical initial systems will retain manual static addressing.

Each future reservation must record:

- Hostname and purpose
- Assigned address and subnet
- VMware adapter MAC address
- Client identifier, where applicable
- Owner and justification
- Change record and validation evidence

Verify reservation behavior in the selected backend. Reserved addresses must not also be available for unrelated dynamic allocation.

Review reservations after VM cloning, adapter replacement, or MAC address changes.

---

# Traffic and Firewall Requirements

DHCPv4 uses UDP server port 67 and client port 68. Initial discovery may use broadcasts before a client has an address.

| Source | Destination | Purpose |
|---|---|---|
| User client on `VMnet3` | Local pfSense User interface | Lease acquisition and renewal |
| Approved testing client on `VMnet5` | Local pfSense Testing interface | Optional lease service |
| pfSense WAN | VMware DHCP on `VMnet8` | WAN lease |
| Domain-joined User clients | `10.10.10.10` | Internal DNS |
| `SLS-WS03` | Approved pfSense management interface | Authorized administration |

Validate backend-generated firewall rules and required local DHCP exchanges.

Do not introduce DHCP relay or broadcast forwarding to compensate for incorrect VMnet placement.

Detailed rules belong in `09-Firewall-Policy-Matrix.md`.

---

# Security Requirements

1. Disable VMware DHCP on all internal VMnets.
2. Enable pfSense DHCP only on approved interfaces.
3. Preserve static gateway, server, and Management addresses.
4. Restrict firewall administration to authorized Management access.
5. Prevent direct bridged or NAT connections that bypass pfSense.
6. Disable internal host virtual adapters unless an approved procedure requires them.
7. Investigate unexpected DHCP offers and duplicate addresses.
8. Monitor pool exhaustion and unfamiliar clients.
9. Preserve Testing isolation.
10. Protect configuration backups and lease evidence.

DHCP reservations and MAC addresses are not reliable identity controls.

Separate VMware networks do not prevent a rogue DHCP server within the same segment. Do not assume physical switch DHCP snooping is present.

---

# Availability and Recovery

The initial environment has one DHCP server and no DHCP failover partner.

Failure of `SLS-FW01` affects routing and lease acquisition or renewal. Existing leases do not restore connectivity when the gateway is unavailable.

Recovery documentation must include:

- Firewall configuration backups
- pfSense version and DHCP backend
- Adapter mappings
- Static interface addresses
- Physical host and pfSense console access
- Restore procedures
- Post-restore lease and conflict checks

Static `SLS-WS03` addressing removes its DHCP dependency but does not restore routing if pfSense is unavailable.

Do not introduce a second DHCP server or overlapping temporary pool without a documented recovery procedure.

---

# Monitoring and Troubleshooting

Review service status, active leases, pool capacity, client identifiers, and relevant DHCP logs.

| Symptom | Initial Checks |
|---|---|
| No usable lease or self-assigned address | Adapter connection, VMnet, interface, service state, available pool |
| Unexpected subnet or gateway | Competing DHCP server, wrong VMnet, unintended NAT or bridged adapter |
| Valid lease but DNS failure | Assigned DNS server, firewall policy, DNS availability, suffix |
| Domain join failure | DNS records, AD traffic, credentials, time alignment |
| Duplicate address | Static address inside pool, duplicate mapping, cloned VM identity |
| Renewal failure after adapter change | MAC/client identifier and reservation mapping |
| Testing cannot reach the domain controller | Confirm intended isolation before treating the block as a fault |

Troubleshooting must preserve security boundaries. Do not enable internal VMware DHCP, add a second workstation adapter, or permit unrestricted inter-network access as a workaround.

---

# Future Networks and Azure

The following networks remain reserved without active DHCP scopes:

| Future VLAN ID | Function | Subnet |
|---|---|---|
| 40 | Security Operations | `10.10.40.0/24` |
| 50 | Investigations | `10.10.50.0/24` |
| 70 | Storage / Backup | `10.10.70.0/24` |
| 80 | Network Infrastructure | `10.10.80.0/24` |

Future VLAN identifiers 10, 20, 30, and 60 correspond to the existing Infrastructure, User, Management, and Testing subnet plan.

VMnet identifiers are not VLAN IDs. No IEEE 802.1Q tagging is required initially.

On-premises address space:

`10.10.0.0/16`

Reserved Azure address space:

`10.20.0.0/16`

Do not extend on-premises DHCP pools into Azure or assume DHCP broadcasts traverse a VPN. Azure address assignment and hybrid DNS require separate designs.

---

# Implementation Dependencies

Before deployment:

- Confirm VMware Workstation Pro and pfSense compatibility.
- Record the DHCP backend and supported settings.
- Verify all five pfSense adapter mappings.
- Configure static internal gateway addresses.
- Disable internal VMware DHCP.
- Confirm non-overlapping `VMnet8` addressing.
- Document critical static addresses.
- Complete the DNS namespace and forwarding design.
- Establish required DNS and Active Directory firewall policy.
- Confirm console recovery and configuration backup procedures.
- Review optional Testing scope settings before activation.

---

# Implementation Documentation

Detailed deployment steps belong in the implementation playbooks.

The DHCP playbook must include:

1. Prerequisites and software versions.
2. VMware DHCP disablement procedures.
3. MAC-to-interface mappings.
4. Static interface and endpoint settings.
5. Backend and scope configuration steps.
6. Final DNS and suffix values.
7. Activation and service checks.
8. Client lease acquisition and renewal procedures.
9. Expected results and evidence.
10. Troubleshooting, backup, rollback, and change records.

The environment must be reproducible from a clean starting point.

---

# Validation Requirements

All tests remain **Not Tested**.

Record expected results, actual results, date, configuration version, evidence, and pass/fail status in `12-Network-Validation-and-Test-Plan.md`.

| Test | Expected Result |
|---|---|
| Internal VMware DHCP inspection | Disabled on `VMnet2` through `VMnet5` |
| pfSense WAN lease | Correct non-overlapping VMware lease |
| `SLS-WS01` lease | Address in User pool; correct mask, gateway, and DNS |
| `SLS-WS02` lease | Distinct valid address and correct options |
| DHCP server identity | Only approved pfSense offers on User network |
| Lease renewal | Successful renewal with valid settings |
| Critical static addresses | Unchanged and excluded from dynamic allocation |
| `SLS-WS03` inspection | Exclusively `VMnet4`, static `10.10.30.10/24` |
| Disabled scope inspection | Infrastructure and Management scopes inactive |
| DNS resolution | Internal and external resolution follows approved design |
| Domain services | Required authentication and Group Policy traffic succeeds |
| Unauthorized Management access | Blocked according to firewall policy |
| Optional Testing scope | Correct options and preserved isolation |
| Logs | Relevant lease activity and faults identifiable |
| Controlled service restart | Correct scopes return without competing offers |
| Backup and recovery | Configuration recoverable through documented procedures |

Optional Testing tests may be marked Not Applicable only when the scope is intentionally disabled and the reason is recorded.

Disruptive recovery tests require a documented test window and rollback procedure.

---

# Change Management

Changes requiring review include:

- DHCP ownership or backend
- Scope activation and pool boundaries
- Lease duration and options
- DNS or gateway settings
- Static addresses and reservations
- Adapter identities and interface mappings
- VMware DHCP state
- Relay behavior or new networks

Review active leases before changing a pool.

Disabling a scope does not immediately remove settings already held by clients. Change procedures must address renewals, lease expiry, and rollback.

Update affected addressing plans, diagrams, designs, playbooks, and validation records together.

---

# Design Decisions

## DD-DHCP-001 — Service Ownership

**Decision:** Use pfSense for approved internal DHCP scopes.

**Reason:** Aligns address assignment with directly connected security zones.

**Status:** Planned — Pending Implementation

## DD-DHCP-002 — User Pool

**Decision:** Use `10.10.20.100 – 10.10.20.199`.

**Reason:** Provides sufficient initial capacity while preserving fixed-address space.

**Status:** Planned — Pending Implementation

## DD-DHCP-003 — Static Infrastructure and Management

**Decision:** Keep Infrastructure and Management DHCP disabled initially.

**Reason:** Preserves predictable critical system and administrative addresses.

**Status:** Planned — Pending Implementation

## DD-DHCP-004 — Testing Scope

**Decision:** Require approval of the testing use case, pool, DNS, and firewall policy before activation.

**Reason:** Preserves default testing isolation.

**Status:** Planned — Pending Scope Review

---

# Completion Criteria

The DHCP design is ready for implementation when:

- Service ownership and interface mappings are documented.
- User scope settings are reviewed.
- Static addressing is preserved.
- Internal VMware DHCP disablement is documented.
- Final DNS settings are resolved.
- Firewall requirements are established.
- Testing activation conditions are defined.
- Implementation and recovery procedures are available.
- Validation criteria are documented.

Design readiness, deployment completion, and validation acceptance must be tracked separately.

---

# Document Status

**Project:** Stoneleaf Services

**Document:** 06 — DHCP Design

**Phase:** Network Design

**Status:** Planned — Pending Implementation Review

**Implementation Status:** Not Started

**Validation Status:** Not Tested

**Previous Document:** `05-VLAN-and-Virtual-Network-Design.md`

**Next Document:** `07-DNS-Design.md`
