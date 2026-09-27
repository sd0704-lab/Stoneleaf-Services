# Stoneleaf Services — Documentation Standards

**No Stone Left Unturned**

## Purpose

This document establishes documentation standards for Stoneleaf Services.

Documentation is considered a core component of technical work rather than an activity performed only after implementation.

These standards are intended to ensure Stoneleaf Services documentation is:

- Accurate
- Consistent
- Organized
- Reproducible
- Maintainable
- Secure
- Professional
- Useful for troubleshooting
- Useful for training
- Suitable for portfolio presentation where appropriate

These standards apply to infrastructure, networking, systems administration, cybersecurity, troubleshooting, digital investigations, intelligence analysis, cloud infrastructure, projects, and future professional services.

---

# Documentation Philosophy

Stoneleaf Services follows a documentation-first approach.

Whenever practical, technical work should follow the sequence:

1. Define the requirement.
2. Design the solution.
3. Document the implementation plan.
4. Implement the solution.
5. Validate the implementation.
6. Troubleshoot unexpected results.
7. Document the final configuration.
8. Record lessons learned.
9. Update affected documentation.

Documentation should describe the environment that actually exists rather than only the environment originally planned.

---

# Documentation Objectives

Stoneleaf Services documentation should make it possible to determine:

- What a system or process does
- Why it exists
- How it is designed
- How it is configured
- What dependencies it has
- How it should be implemented
- How proper operation is verified
- How it should be administered
- How failures can be diagnosed
- How changes are recorded
- How the system can be recovered
- What was learned during implementation

A technically competent person should be able to use the documentation to understand the environment without relying entirely on undocumented knowledge.

---

# Documentation Platforms

Stoneleaf Services will maintain two primary documentation layers.

## GitHub Documentation

GitHub will serve as the primary repository for:

- Architecture documentation
- Requirements
- Design documentation
- Technical summaries
- Sanitized configuration examples
- Network diagrams
- Troubleshooting case studies
- Sanitized incident reports
- Sanitized investigation reports
- Projects
- Scripts
- Templates
- Portfolio materials

GitHub documentation should be polished, professional, readable, and suitable for public presentation.

Sensitive information must not be included in the public repository.

---

## Detailed Private Runbooks

Detailed implementation and operational runbooks may be maintained in Microsoft Word and stored in appropriate private storage.

Private runbooks may contain:

- Detailed installation procedures
- Click-by-click instructions
- Configuration procedures
- Screenshots
- Verification procedures
- Troubleshooting procedures
- Recovery procedures
- Administrative procedures
- Detailed implementation notes
- Lessons learned

Private runbooks are intended to provide sufficient detail to reproduce a configuration from beginning to end.

---

# Documentation Separation

GitHub documentation and private runbooks serve different purposes.

## GitHub

GitHub answers questions such as:

- What was built?
- Why was it built?
- How was it designed?
- What technologies were used?
- How was it secured?
- How was it validated?
- What problems were encountered?
- What was learned?

## Private Runbooks

Private runbooks answer questions such as:

- Exactly where do I click?
- What option do I select?
- What value do I enter?
- What command do I execute?
- What output should I expect?
- What screenshot confirms the result?
- What do I do if the step fails?
- How do I reverse the change?

The public repository should not become a collection of oversized screenshot-based installation manuals when a concise technical explanation is more appropriate.

---

# Repository Structure

The Stoneleaf Services GitHub repository will use the following primary structure:

```text
Stoneleaf-Services/
│
├── README.md
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
└── screenshots/
