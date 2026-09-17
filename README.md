# Northstar Consulting — Microsoft 365 Administration Lab

A hands-on administration case study for a fictional company, focused on skills relevant to **entry-level IT Support and Microsoft 365 support**.

## Project context

This lab covers the identity, collaboration, security, and delegated administration functions of a Microsoft 365 environment. The business scenario is a small consulting company requiring organizational accounts, shared communication and collaboration resources, and controlled access.

The lab has been reported complete by its author. Portfolio documentation is being developed and reviewed one phase at a time. Specific configuration and test claims are included only where supported by supplied evidence.

## Case study approach

Each phase explains the business requirement, implementation, validation, troubleshooting, and skills demonstrated. Screenshots support the narrative and are interpreted with clear limits on what they prove.

## Project scope

| Phase | Area | Documentation |
| --- | --- | --- |
| 1 | Identity and user provisioning | [Case study — approved](docs/phase-01-identity-and-user-provisioning.md) |
| 2 | Security groups and Microsoft 365 groups | [Case study — approved](docs/phase-02-security-and-microsoft-365-groups.md) |
| 3 | Exchange Online and shared mailboxes | [Case study — approved](docs/phase-03-exchange-online-and-shared-mailboxes.md) |
| 4 | Microsoft Teams | [Case study — approved](docs/phase-04-microsoft-teams.md) |
| 5 | SharePoint Online | [Case study — approved](docs/phase-05-sharepoint-online.md) |
| 6 | MFA and Conditional Access | [Case study — ready for review](docs/phase-06-mfa-and-conditional-access.md) |
| 7 | Self-Service Password Reset | Reserved for a later review |
| 8 | RBAC, administrative delegation and auditing | Reserved for a later review |

## Current evidence

Phase 1 includes three screenshots: eight Member accounts with consistent UPNs and no on-premises synchronization, Alex Morgan's user profile, and Alex Morgan's active Microsoft 365 E5 Developer license with direct assignment. The case study distinguishes observed configuration from sign-in tests, provisioning methods, and troubleshooting outcomes that have not yet been provided.

Phase 2 includes five screenshots documenting four department security groups, three Microsoft 365 collaboration groups, and HR group membership and ownership. All seven groups show Assigned membership. The case study explains each group type's purpose and distinguishes configuration checks from resource access testing.

Phase 3 includes nine screenshots covering HR, Finance, and IT Support shared mailboxes, HR and IT Support delegation, and the HR end-user validation. It distinguishes Full Access from Send As and documents the received HR test message, with clear limits on Finance permissions and the Outlook access capture.

Phase 4 includes six screenshots covering the HR, Finance, and Sales teams, HR's standard and private channels, team roles, and HR Management membership. Sarah's and Melissa's identified user views show the expected difference in private-channel visibility.

Phase 5 documents the Northstar Corporate Portal, four document libraries, HR's unique permissions, and the SG-HR-Users Edit assignment. The Sarah-versus-James comparison records portal visibility rather than a direct library allow/deny test. Six supplied screenshots accompany the case study.

Phase 6 includes five screenshots covering enabled CA001 and CA002 policies and Sarah's sign-in evaluations. It documents the author-reported Report-only rollout, CA001's Success result, and CA002's expected Not Applied result for a Browser client, with unshown exclusion identities and test details left unspecified.

## Relevance to support roles

This project provides a context for discussing user account administration, Microsoft 365 service support, access troubleshooting, and clear technical documentation. Evidence and demonstrated skills are described within each phase rather than assuming every listed technology has been independently validated.

## Lab and privacy boundary

Northstar Consulting is fictional. This repository describes lab work and does not represent a production customer deployment.

Only reviewed evidence belongs in this portfolio. Passwords, MFA secrets, QR codes, tokens, personal phone numbers, recovery information, and other credentials must not be committed.

**Current review boundary: Phases 1–5 approved; Phase 6 ready for review. Phase 7 has not been started.**
