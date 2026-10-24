# Stoneleaf Services — Routing and NAT Design

**No Stone Left Unturned**

## Purpose

This document defines the planned routing and Network Address Translation (NAT) architecture for Stoneleaf Services.

It builds on:

- `05-VLAN-and-Virtual-Network-Design.md`
- `06-DHCP-Design.md`
- `07-DNS-Design.md`

The design establishes gateway assignments, internal routing, outbound NAT, external connectivity, security boundaries, future hybrid connectivity, and validation requirements.

All configurations remain **planned** until implemented and validated. Documented routes and traffic paths do not establish that connectivity is operational.

---

# Design Objectives

The routing and NAT design must:

1. Centralize inter-network routing through pfSense.
2. Preserve separate Infrastructure, User Endpoint, Management, and Testing networks.
3. Provide approved outbound internet connectivity.
4. Prevent alternate paths that bypass firewall enforcement.
5. Preserve original source addresses between internal networks.
6. Avoid overlapping internal, upstream, and future Azure address spaces.
7. Support internal DNS and Active Directory communication.
8. Maintain controlled administrative access.
9. Support repeatable troubleshooting and recovery.
10. Provide a foundation for future VPN and Azure connectivity.

---

# Design Principles

## Routing and Authorization Are Separate

A route identifies a potential forwarding path.

Firewall policy determines whether traffic may use that path.

The presence of a directly connected route must not be interpreted as permission for unrestricted communication.

## Centralized Internal Gateway

`SLS-FW01` will provide the default gateway for each internal network.

Servers and workstations must not provide routing, bridging, Internet Connection Sharing, or alternate gateways between security zones.

## NAT at the External Boundary

Outbound NAT will support approved internet access.

Traffic between internal networks will retain its original source address and remain subject to firewall policy.

## Documentation Before Configuration

Routes, gateways, NAT behavior, exceptions, and dependencies must be documented before activation.

Implementation settings and validation evidence will be recorded separately.

---

# Approved Virtual Network Architecture

Stoneleaf Services will use VMware Workstation Pro on a single physical Windows host.

| VMware Network | Type | Function | Subnet |
|---|---|---|---|
| `VMnet8` | NAT | WAN / External Connectivity | VMware-assigned |
| `VMnet2` | Custom Host-Only | Infrastructure | `10.10.10.0/24` |
| `VMnet3` | Custom Host-Only | User Endpoints | `10.10.20.0/24` |
| `VMnet4` | Custom Host-Only | Management | `10.10.30.0/24` |
| `VMnet5` | Custom Host-Only | Lab / Testing | `10.10.60.0/24` |

Internal networks must not use VMware NAT or direct bridging to the physical network.

VMware DHCP must remain disabled on the four internal VMnets.

Internal host virtual adapters must remain disabled unless a documented administrative procedure requires them.

The initial architecture does not require IEEE 802.1Q VLAN tagging.

---

# Routing Platform

## Primary Router and Firewall

| Setting | Planned Value |
|---|---|
| Hostname | `SLS-FW01` |
| Platform | pfSense |
| Virtual adapters | Five |
| Routing role | Central router for all initial internal networks |
| NAT role | Outbound translation toward `VMnet8` |
| Upstream connection | VMware NAT |

Only `SLS-FW01` will connect directly to multiple Stoneleaf Services security zones.

The selected pfSense version, adapter types, and interface mappings must be recorded during implementation.

---

# pfSense Interface Assignments

| Logical Interface | VMware Network | Address Configuration | Function |
|---|---|---|---|
| WAN | `VMnet8` | VMware DHCP | Upstream connectivity |
| LAN / Infrastructure | `VMnet2` | `10.10.10.1/24` | Infrastructure gateway |
| OPT1 / User Endpoints | `VMnet3` | `10.10.20.1/24` | User gateway |
| OPT2 / Management | `VMnet4` | `10.10.30.1/24` | Management gateway |
| OPT3 / Lab / Testing | `VMnet5` | `10.10.60.1/24` | Testing gateway |

These are logical assignments.

VMware MAC addresses must be matched to actual pfSense interface identifiers during deployment. Adapter enumeration must not be assumed.

Internal interfaces must not be assigned an upstream gateway.

The WAN default gateway will be learned through the VMware DHCP configuration.

---

# Endpoint Gateway Assignments

| System | Network | Address | Default Gateway |
|---|---|---|---|
| `SLS-DC01` | Infrastructure | Static `10.10.10.10` | `10.10.10.1` |
| `SLS-LNX01` | Infrastructure | Static `10.10.10.20` | `10.10.10.1` |
| `SLS-WS01` | User Endpoints | DHCP | `10.10.20.1` |
| `SLS-WS02` | User Endpoints | DHCP | `10.10.20.1` |
| `SLS-WS03` | Management | Static `10.10.30.10` | `10.10.30.1` |
| Approved Testing systems | Lab / Testing | Defined per test | `10.10.60.1`, when routed access is required |

All initial internal networks use:

`255.255.255.0`

`SLS-WS03` must remain connected exclusively to `VMnet4`.

Do not add a second adapter or alternate default gateway to bypass a routing or firewall problem.

---

# Expected Routing Table

The initial pfSense routing table should contain directly connected routes for:

| Destination | Path |
|---|---|
| `10.10.10.0/24` | Infrastructure interface |
| `10.10.20.0/24` | User Endpoint interface |
| `10.10.30.0/24` | Management interface |
| `10.10.60.0/24` | Lab / Testing interface |
| Actual VMware NAT subnet | WAN interface |
| `0.0.0.0/0` | VMware NAT gateway through WAN |

The exact WAN subnet and gateway remain implementation values.

No static routes are required between the four initial internal networks because they are directly connected to pfSense.

Do not add static routes for directly connected networks as a substitute for correcting interface configuration.

---

# Internal Routing Architecture

## Cross-Network Traffic

The expected path between internal security zones is:

**Source System → Local pfSense Gateway → Firewall Policy → Destination Network → Destination System**

Example:

**SLS-WS03 → 10.10.30.1 → pfSense Policy → VMnet2 → SLS-DC01**

The destination system returns traffic through its own local pfSense gateway.

Correct endpoint gateways are necessary to preserve the return path.

## Same-Network Traffic

Systems on the same subnet communicate directly through their VMware Layer 2 segment.

For example:

**SLS-DC01 ↔ VMnet2 ↔ SLS-LNX01**

This traffic does not normally traverse pfSense.

Host firewalls and endpoint controls must enforce applicable same-segment restrictions.

## Internal NAT Policy

Do not apply source NAT between the initial internal networks.

Preserving source addresses supports:

- Accurate firewall and server logs
- Source-specific access rules
- Administrative accountability
- Troubleshooting
- Clear security boundaries

Any future internal NAT exception requires a documented technical requirement and review.

---

# External Connectivity

## Outbound Traffic Path

The expected internet path is:

**Internal System → pfSense Internal Gateway → pfSense Outbound NAT → VMnet8 → VMware NAT → Physical Host Network → Internet**

Two translation layers are expected:

1. pfSense translates the internal source address to its WAN address.
2. VMware NAT translates the pfSense WAN traffic for upstream connectivity.

This double NAT arrangement is acceptable for the initial environment.

Additional upstream translation may exist outside the lab and must not be assumed to be under Stoneleaf Services control.

## WAN Address Selection

The VMware NAT subnet must not overlap:

- On-premises Stoneleaf Services space: `10.10.0.0/16`
- Reserved Azure space: `10.20.0.0/16`
- The physical upstream network
- Other relevant VPN or host-connected networks

Record the actual subnet, VMware NAT gateway, DHCP range, pfSense lease, and lease behavior during implementation.

---

# Outbound NAT Design

## Initial Configuration Approach

Use pfSense Automatic Outbound NAT initially.

Inspect the generated rules and verify that every intended internal source network is covered when using the WAN path.

Do not assume that configuration mode alone proves correct translation.

Hybrid or Manual Outbound NAT may be introduced only when a documented requirement cannot be met by the initial mode.

## Required Translation Behavior

| Source Network | Destination | Translation | Additional Requirement |
|---|---|---|---|
| Infrastructure | Approved external destinations | pfSense WAN address | Firewall permission |
| User Endpoints | Approved external destinations | pfSense WAN address | Firewall permission |
| Management | Approved external destinations | pfSense WAN address | Restricted administrative use |
| Lab / Testing | Approved external destinations | pfSense WAN address | Explicit testing approval |
| Any internal network | Another internal network | None | Explicit firewall permission |

NAT coverage does not authorize traffic.

A Testing network may appear in generated outbound NAT rules while its firewall policy continues to deny external access.

## Port Translation

Use the default outbound port translation behavior initially.

Do not enable static-port NAT without a specific application requirement and validation.

Document any exception by source, destination, protocol, purpose, and expected behavior.

---

# WAN Security Configuration

The pfSense WAN will normally receive a private IPv4 address from VMware NAT.

The WAN private-network blocking setting must be reviewed and configured to permit the intended private upstream environment.

This adjustment does not authorize general inbound WAN access.

Review other WAN filtering settings against the selected address space and installed pfSense version. Do not disable protections indiscriminately.

Unsolicited inbound WAN traffic remains denied unless a separately approved requirement defines an exception.

---

# Firewall Policy Dependencies

Routing and outbound NAT must be supported by least-privilege firewall rules.

The implementation must not retain broad installation defaults that contradict the approved security boundaries.

In particular, review:

- Default LAN allow rules
- Rules on newly enabled optional interfaces
- Firewall administration access
- Automatic and anti-lockout rules
- DNS and AD access
- Internet egress
- Logging
- Access to the physical upstream network

The Infrastructure interface is logically assigned as LAN. Any default LAN rule must therefore be reviewed as an Infrastructure rule rather than assumed appropriate.

Before restricting administrative rules, establish and verify the approved Management access path and console recovery procedure.

Detailed rules belong in:

`09-Firewall-Policy-Matrix.md`

---

# Internal Service Traffic

## Active Directory and DNS

User workstations and `SLS-WS03` require approved access to `SLS-DC01`.

DNS server:

`10.10.10.10`

Routing must support the required DNS and AD paths without translating internal source addresses.

DNS access alone does not provide complete domain connectivity. Required authentication, domain joining, Group Policy, time, and administration traffic must be defined separately.

## Linux Administration

Approved SSH administration of `SLS-LNX01` will originate from authorized Management systems.

Expected path:

**SLS-WS03 → Management Gateway → pfSense Policy → 10.10.10.20**

## Firewall Administration

`SLS-WS03` will access the approved pfSense Management address:

`10.10.30.1`

Traffic to pfSense itself is firewall-local traffic, not ordinary forwarding between two endpoint networks.

Administration services and allowed source identities must be defined explicitly.

---

# Management Network Routing

The Management network is:

`10.10.30.0/24`

`SLS-WS03` is the dedicated administrative workstation:

`10.10.30.10`

Management systems may reach only approved destinations and services.

User and Testing systems must not receive unrestricted access to Management.

The Management workstation must not provide:

- IP forwarding
- Network bridging
- Internet Connection Sharing
- A proxy route between security zones
- An alternate path through a second adapter

VMware Workstation Pro and physical host administration remain separate from guest Management access.

---

# Lab / Testing Routing

The Testing network is:

`10.10.60.0/24`

Its pfSense gateway is:

`10.10.60.1`

Testing access to Infrastructure and Management is denied by default.

External access may be permitted for documented software installation, updates, and training requirements.

Higher-risk systems may require external access to remain disabled.

Testing rules must consider all protected destinations, including:

- Stoneleaf Services internal networks
- The physical host network
- Other upstream private networks
- Future VPN-connected networks
- Firewall administration addresses

A general WAN route must not be treated as permission to access the physical upstream environment.

Testing DNS must follow `07-DNS-Design.md`. Do not grant Infrastructure DNS access implicitly.

---

# Inbound NAT and Published Services

The initial design does not require inbound internet services.

The following will remain unconfigured:

- WAN port forwards to internal systems
- One-to-one NAT
- Internet-published administrative services
- VMware NAT inbound forwards for Stoneleaf Services
- Automatic port-mapping services such as UPnP/NAT-PMP

A future published service requires a documented destination, business purpose, security review, firewall policy, monitoring, and validation plan.

With double NAT, inbound connectivity may require coordinated configuration at multiple boundaries. A pfSense port forward alone does not establish end-to-end internet reachability.

Do not expose Remote Desktop, SSH, or the pfSense administrative interface as a convenience workaround.

---

# NAT Reflection and Internal Service Access

No NAT reflection requirement exists initially because no internet-published internal service is planned.

Internal clients should use approved internal DNS names and direct routed access.

If a future service uses the same hostname internally and externally, evaluate split DNS before introducing reflection.

Document certificate, namespace, routing, and access implications before implementation.

---

# Static Routes and Policy Routing

## Initial Static Routes

No additional static routes are required initially.

The initial deployment does not activate routes to reserved future networks or Azure.

## Policy Routing

No policy routing, gateway groups, multi-WAN, or load balancing is planned.

Internal firewall rules should use ordinary routing-table behavior unless a documented exception is introduced.

Selecting a gateway on a rule can change forwarding behavior and must not be used casually to solve connectivity problems.

## Asymmetric Routing

Avoid configurations where traffic reaches a destination through one path and returns through another.

Review endpoint gateways, secondary adapters, host routes, VPN clients, and forwarding settings when diagnosing asymmetric traffic.

---

# IPv6 Scope

This document defines the initial IPv4 routing and NAT architecture.

No IPv6 routing, router advertisement, DHCPv6, or IPv6 NAT capability is authorized by this design.

Before deployment, make and document an explicit IPv6 handling decision for pfSense and endpoints.

IPv6 must not create an unreviewed alternate path. Do not indiscriminately disable endpoint IPv6 without considering platform and service dependencies.

---

# Future Networks and VLANs

The following networks remain reserved:

| Future VLAN ID | Function | Subnet |
|---|---|---|
| 40 | Security Operations | `10.10.40.0/24` |
| 50 | Investigations | `10.10.50.0/24` |
| 70 | Storage / Backup | `10.10.70.0/24` |
| 80 | Network Infrastructure | `10.10.80.0/24` |

Future VLAN identifiers 10, 20, 30, and 60 correspond to the existing Infrastructure, User, Management, and Testing addressing plan.

Reserved networks are not directly connected routes in the initial deployment.

Do not create placeholder interfaces, gateways, or active routes for them.

Future activation requires:

- Documented purpose
- Interface or VLAN design
- Gateway assignment
- Routing review
- NAT review
- Firewall policy
- DHCP and DNS decisions
- Updated diagrams
- Validation procedures

The five-NIC initial firewall model must not be silently expanded.

---

# Future Azure and VPN Connectivity

On-premises address space:

`10.10.0.0/16`

Reserved Azure address space:

`10.20.0.0/16`

No Azure VPN or operational cloud route is implemented by this document.

Future hybrid connectivity must define:

- Actual deployed Azure prefixes
- Tunnel technology and endpoints
- Upstream NAT traversal requirements
- Authentication and cryptographic settings
- Forward and return routes
- Firewall rules
- NAT exemption or translation behavior
- DNS integration
- Monitoring and recovery

Preserve original on-premises addresses across the VPN where the approved tunnel design requires it.

NAT exclusions must be reviewed explicitly when the VPN is introduced. Do not assume the initial internet NAT rules are suitable for hybrid traffic.

Advertise or route only approved prefixes. Reserved aggregate space does not establish that every subnet is deployed or reachable.

Double NAT may affect VPN establishment and inbound reachability. Validate the selected design end to end.

---

# Availability and Recovery

`SLS-FW01` is the single routing and NAT dependency for the initial environment.

Its failure affects:

- Cross-network communication
- Internet connectivity
- Approved internal DHCP services
- Access to services located on other segments

Same-segment communication may remain available, subject to endpoint configuration.

Recovery documentation must include:

- pfSense configuration backups
- Installed version
- Interface MAC mappings
- Static interface addresses
- VMware NAT configuration
- Firewall and NAT settings
- Physical host console access
- Restore and post-restore checks

Changes to routes, NAT, or rules may affect existing state-table entries.

Document whether selective state removal is required during a change. Clearing all states is disruptive and must not be a routine first troubleshooting step.

---

# Monitoring and Troubleshooting

Review:

- Interface status
- WAN lease and gateway
- Routing table
- Firewall rules and logs
- Outbound NAT rules
- State-table entries
- Endpoint address and gateway
- DNS settings
- Packet captures where required

| Symptom | Initial Checks |
|---|---|
| Same-subnet communication fails | VMnet placement, mask, adapter state, endpoint firewall |
| Cross-network communication fails | Endpoint gateway, destination gateway, pfSense policy, endpoint service |
| All external access fails | WAN lease, upstream gateway, VMware NAT, physical host connectivity |
| One network lacks internet access | Source rule, NAT coverage, gateway settings |
| IP access works but names fail | Client DNS, internal DNS access, forwarders |
| Traffic works only in one direction | Stateful policy, return route, asymmetric paths |
| Testing reaches protected systems | Rule order, aliases, broad permits, alternate adapters |
| Changes appear ineffective | Existing states, wrong interface, wrong rule or route |
| WAN gateway monitor reports failure | Monitoring target and upstream response behavior |

A failed ping does not by itself prove that routing is broken.

Separate name resolution, transport reachability, service availability, and firewall behavior during investigation.

Do not troubleshoot by enabling unrestricted access or creating an alternate network path.

---

# Implementation Dependencies

Before deployment:

- Confirm VMware Workstation Pro compatibility.
- Verify five pfSense adapters.
- Record MAC-to-interface mappings.
- Select a non-overlapping VMware NAT subnet.
- Confirm WAN DHCP and upstream gateway behavior.
- Configure internal static interfaces.
- Configure endpoint gateways.
- Disable internal VMware DHCP.
- Review host adapters and host forwarding.
- Define required firewall traffic.
- Confirm DNS and AD dependencies.
- Establish Management and console recovery access.
- Record the IPv6 handling decision.

---

# Implementation Documentation

The implementation playbook must include:

1. Software versions and prerequisites.
2. VMware virtual network configuration.
3. Adapter mappings.
4. pfSense interface configuration.
5. WAN DHCP and gateway verification.
6. Endpoint gateway settings.
7. Outbound NAT mode and generated-rule inspection.
8. Firewall rule configuration.
9. Management access verification.
10. Positive and negative connectivity tests.
11. Configuration backups.
12. Troubleshooting and rollback procedures.

Record exact settings and evidence rather than assuming default behavior.

---

# Validation Requirements

All tests remain **Not Tested**.

Record expected results, actual results, date, configuration version, evidence, and pass/fail status in:

`12-Network-Validation-and-Test-Plan.md`

| Test ID | Test | Expected Result |
|---|---|---|
| RT-01 | Inspect VMware mappings | Correct five-network architecture |
| RT-02 | Inspect pfSense interfaces | Correct WAN and four internal assignments |
| RT-03 | Inspect WAN lease | Valid non-overlapping address and gateway |
| RT-04 | Inspect routing table | Four connected internal routes and correct default route |
| RT-05 | Inspect endpoint gateways | Correct local pfSense gateway on each system |
| RT-06 | Validate approved cross-network traffic | Permitted services reachable through pfSense |
| RT-07 | Validate blocked cross-network traffic | Unauthorized communication denied |
| RT-08 | Inspect internal source addresses | No source NAT between internal networks |
| RT-09 | Validate approved internet access | Correct outbound translation and return traffic |
| RT-10 | Inspect NAT coverage | Intended source networks covered without implying permission |
| RT-11 | Inspect `SLS-WS03` | Exclusively `VMnet4`, static `10.10.30.10` |
| RT-12 | Validate Management access | Approved administration succeeds; unauthorized access fails |
| RT-13 | Validate Testing restrictions | Infrastructure and Management denied by default |
| RT-14 | Validate upstream private-network restrictions | Physical host and other protected destinations inaccessible unless approved |
| RT-15 | Inspect inbound exposure | No unapproved pfSense or VMware port forwards |
| RT-16 | Check alternate paths | No endpoint bridging, host routing, or unintended secondary adapters |
| RT-17 | Validate DNS and AD dependencies | Required services work across approved boundaries |
| RT-18 | Inspect reserved networks | No unapproved active interfaces or routes |
| RT-19 | Review logs and states | Traffic decisions can be traced |
| RT-20 | Validate recovery procedure | Configuration restored and required paths reverified |

Do not claim that same-subnet traffic is filtered by pfSense.

Optional VPN tests remain outside initial acceptance until a VPN design is approved.

Disruptive outage and recovery tests require a documented recovery path.

---

# Change Management

Review changes involving:

- VMware network assignments
- Interface addresses
- WAN addressing
- Default gateways
- Static routes
- Policy routing
- Outbound NAT mode
- Port forwards
- Static-port exceptions
- VPN routes
- VLAN activation
- Host forwarding
- IPv6 behavior

Each change must include:

- Purpose
- Affected systems and traffic
- Configuration backup
- Expected behavior
- Verification steps
- Rollback procedure
- Updated documentation

Update diagrams, addressing plans, firewall policies, implementation playbooks, and validation records together.

---

# Design Decisions

## DD-RT-001 — Central Routing

**Decision:** Use `SLS-FW01` as the router for all initial internal networks.

**Reason:** Provides a consistent enforcement and troubleshooting point.

**Status:** Approved Architecture — Pending Implementation

## DD-RT-002 — Internal Address Preservation

**Decision:** Do not use NAT between initial internal networks.

**Reason:** Preserves source identity and clear policy enforcement.

**Status:** Planned — Pending Validation

## DD-RT-003 — External Connectivity

**Decision:** Use pfSense outbound NAT through VMware `VMnet8` NAT.

**Reason:** Provides practical outbound connectivity for the initial single-host environment.

**Status:** Approved Architecture — Pending Implementation

## DD-RT-004 — Initial Outbound NAT Mode

**Decision:** Begin with Automatic Outbound NAT and verify generated coverage.

**Reason:** Reduces initial configuration complexity while retaining review requirements.

**Status:** Planned — Pending Version and Configuration Verification

## DD-RT-005 — Inbound Services

**Decision:** Do not publish internal services initially.

**Reason:** No documented inbound service requirement exists.

**Status:** Planned — Pending Validation

## DD-RT-006 — Future Hybrid Routing

**Decision:** Reserve Azure `10.20.0.0/16` separately from on-premises `10.10.0.0/16`.

**Reason:** Preserves a foundation for non-overlapping hybrid connectivity.

**Status:** Reserved — No VPN Implemented

---

# Completion Criteria

The routing and NAT design is ready for implementation when:

- Interface assignments are documented.
- WAN addressing requirements are established.
- Internal gateways are defined.
- Expected routes are documented.
- NAT behavior is defined.
- Firewall dependencies are identified.
- Management and Testing restrictions are established.
- Alternate paths are addressed.
- Recovery procedures are available.
- Validation criteria are documented.

Deployment completion requires configuration evidence.

Validation acceptance requires successful recorded tests.

---

# Document Status

**Project:** Stoneleaf Services

**Document:** 08 — Routing and NAT Design

**Phase:** Network Design

**Status:** Planned — Pending Implementation Review

**Implementation Status:** Not Started

**Validation Status:** Not Tested

**Previous Document:** `07-DNS-Design.md`

**Next Document:** `09-Firewall-Policy-Matrix.md`
