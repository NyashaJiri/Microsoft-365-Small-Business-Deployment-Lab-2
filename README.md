# Northstar Consulting — Microsoft 365 Administration Lab

A simulated small-business deployment in a **Microsoft 365 E5 Developer tenant**, demonstrating skills relevant to  **IT Support and Microsoft 365 administration**. Northstar Consulting is fictional, this project represents independent lab work.

## Business scenario and demonstrated skills

Northstar needed organizational accounts, departmental communication and document access, password recovery, and delegated administration. The lab covers **Microsoft Entra ID, Exchange Online, Teams, SharePoint Online, MFA, Conditional Access, SSPR, and role-based access control (RBAC)**.

The strongest demonstrated skills are mailbox delegation, group-based permissions, password-recovery troubleshooting, least-privilege role assignment, and audit/sign-in log interpretation.

## Validated outcomes

- **Password recovery:** Sarah's successful self-service password reset is supported by a Microsoft Entra audit event and a supplied reset-completion screen.
- **Delegated support:** Daniel, assigned Helpdesk Administrator, reset James's password. Audit evidence identifies the actor, target, action, and successful result.
- **Departmental communication:** HR and IT Support have separate Full Access and Send As assignments. A received HR test message displays the departmental sender.
- **Access control:** Sarah sees the HR Management private channel; Melissa's channel list excludes it. HR Documents has unique permissions, with SG-HR-Users assigned Edit.
- **Security and administration:** CA001 records Success with grant controls satisfied; CA002 records Not Applied for a nonmatching Browser client. Alex has four specific administrator roles instead of Global Administrator and demonstrated Teams admin-center access.



## Detailed case studies

Each phase connects the business requirement, configuration, validation, screenshots, and support skills, with troubleshooting where relevant.

| Phase | Case study |
| --- | --- |
| 1 | [Identity and user provisioning](docs/phase-01-identity-and-user-provisioning.md) |
| 2 | [Security groups and Microsoft 365 groups](docs/phase-02-security-and-microsoft-365-groups.md) |
| 3 | [Exchange Online and shared mailboxes](docs/phase-03-exchange-online-and-shared-mailboxes.md) |
| 4 | [Microsoft Teams](docs/phase-04-microsoft-teams.md) |
| 5 | [SharePoint Online](docs/phase-05-sharepoint-online.md) |
| 6 | [MFA and Conditional Access](docs/phase-06-mfa-and-conditional-access.md) |
| 7 | [Self-Service Password Reset](docs/phase-07-self-service-password-reset.md) |
| 8 | [RBAC, administrative delegation, and auditing](docs/phase-08-rbac-delegation-and-auditing.md) |


