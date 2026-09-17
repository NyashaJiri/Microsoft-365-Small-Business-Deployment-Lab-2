# Phase 8 — RBAC, Administrative Delegation, and Auditing

[Back to project overview](../README.md)

## Business requirement

Northstar Consulting needed to delegate routine support and workload administration without giving every administrator Global Administrator access. Support staff needed enough authority to resolve appropriate user issues, while administrators needed access aligned with their assigned services. Administrative actions and sign-in policy evaluations also needed to be traceable.

This phase documents supplied role assignments, Daniel Reed's password-reset validation, Alex Morgan's Teams admin access, and Microsoft Entra audit and Conditional Access evidence.

## Implementation evidenced

### Role-based delegation

Role-based access control (RBAC) assigns administrative capabilities through defined roles. Least privilege means limiting those capabilities to the responsibilities a person needs to perform. In this lab, Daniel received a support role, while Alex received four roles aligned with user and workload administration instead of Global Administrator.

| Administrator | Evidenced role assignment | Intended responsibility |
| --- | --- | --- |
| Daniel Reed — daniel.reed@nyashajiri.com | Helpdesk Administrator | Limited support tasks, demonstrated here by resetting an eligible user's password |
| Alex Morgan — alex.morgan@nyashajiri.com | User Administrator | User administration |
| Alex Morgan | Exchange Administrator | Exchange administration |
| Alex Morgan | Teams Administrator | Teams administration |
| Alex Morgan | SharePoint Administrator | SharePoint administration |

Figures 1 and 3 show **Direct**, **Active** assignments with **Permanent** end times and the displayed scope **MSFT**. Daniel's capture lists Helpdesk Administrator. Alex's capture lists the four roles above and does not list Global Administrator. No removal of a previous Global Administrator assignment is claimed.

Using these roles reduced unnecessary administrative exposure by matching delegated access to support and service responsibilities rather than granting broad tenant administration. Alex's combination still carries significant privileges, and the supplied assignments are permanent; the evidence does not show time-limited activation.

### Audit and sign-in review

The supplied Microsoft Entra audit record links an administrative action to its initiating user, target, and outcome. The separate sign-in policy captures show how Conditional Access evaluated Sarah Johnson's browser access. These records answer different questions: audit logs show the administrative change, while the supplied sign-in views show policy evaluation during access.

## Validation and testing

| Validation | Supplied evidence | Observed result |
| --- | --- | --- |
| Daniel's delegated role | Figure 1 | Helpdesk Administrator is directly assigned and active |
| Helpdesk password reset | Figure 2 | Daniel's session shows James Taylor's profile and the confirmation **Password has been reset** |
| Alex's role configuration | Figure 3 | User, Exchange, SharePoint, and Teams Administrator are active |
| Alex's workload access | Figure 4 | Alex is signed in to the Teams admin center and can view **Manage teams** |
| Administrative audit trail | Figures 5a–5b | Successful **Reset password (by admin)** event identifies Daniel as actor and James as target |
| CA001 evaluation | Figure 6a | Enabled policy returns **Success**, with user/resource matched and grant controls satisfied |
| CA002 evaluation | Figure 6b | Enabled policy returns **Not Applied**; the Browser client does not match its client-app condition |

### Helpdesk action and audit correlation

Figure 2 shows James Taylor (james.taylor@nyashajiri.com) with **0 assigned roles**, and the successful reset confirmation in Daniel's signed-in session. The temporary password is obscured in the supplied screenshot and remains obscured.

The paired audit views record:

| Audit field | Visible value |
| --- | --- |
| Date | September 17, 2026, 2:09 PM; timezone not shown |
| Activity type | Reset password (by admin) |
| Category | UserManagement |
| Status | success |
| Status reason | Successfully completed reset. |
| Initiating user | daniel.reed@nyashajiri.com |
| Target | James Taylor — james.taylor@nyashajiri.com |

Together, the interface confirmation and audit details support the successful delegated reset. No subsequent sign-in by James or additional helpdesk action is shown.

### Workload access

Figure 4 identifies Alex Morgan in the Teams admin center and displays the Finance, HR, and Sales teams under **Manage teams**. This validates access to the Teams administration view. It does not show a team change.

The other three administrator assignments are evidenced in Figure 3, but separate access tests for Exchange, SharePoint, and user administration were not supplied. Their role assignments are documented without claiming successful tests for those workloads.

### Authentication and Conditional Access evidence

Figures 6a and 6b concern **Sarah Johnson**, with **Windows Azure Active Directory** as the matched resource and **Browser** as the client app.

- **CA001 – Require MFA – All Users:** policy state **Enabled**, result **Success**, and **Grant Controls: Satisfied**.
- **CA002 – Block Legacy Authentication:** policy state **Enabled**, result **Not Applied**, and Browser **Not matched** under Client app.

CA002's result is consistent with the normal browser sign-in falling outside the policy's targeted client-app condition. It is not evidence of a blocked legacy-authentication attempt.

These captures show Conditional Access outcomes. They do not expose Authentication Details, the method used, or whether a fresh MFA prompt occurred. They are separate from Daniel's reset audit and Alex's administration view, and are not presented as sign-in validation for either administrator.

## Screenshots and evidence

All eight supplied screenshots are stored in [the Phase 8 RBAC/auditing screenshots directory](../screenshots/phase-08-rbac-auditing/). They are retained as supplied, including existing obscuring of the temporary password.

### Figure 1 — Daniel's delegated role

![Daniel Reed's active Helpdesk Administrator assignment](../screenshots/phase-08-rbac-auditing/01-daniel-helpdesk-role.png)

*Direct, active Helpdesk Administrator assignment with a Permanent end time.*

### Figure 2 — Helpdesk password-reset validation

![Daniel's session showing a successful password reset for James Taylor](../screenshots/phase-08-rbac-auditing/02-helpdesk-password-reset-validation.png)

*The reset confirmation is visible; the supplied image obscures the temporary password.*

### Figure 3 — Alex's administrator roles

![Alex Morgan's four active administrator roles](../screenshots/phase-08-rbac-auditing/03-alex-admin-roles.png)

*User, Exchange, SharePoint, and Teams Administrator are listed; Global Administrator is not listed.*

### Figure 4 — Alex's Teams admin access

![Alex Morgan viewing Manage teams in the Teams admin center](../screenshots/phase-08-rbac-auditing/04-alex-admin-access-validation.png)

*The identified session can view the three departmental teams.*

### Figure 5a — Audit activity and actor

![Successful administrative password-reset audit event initiated by Daniel Reed](../screenshots/phase-08-rbac-auditing/05a-audit-log-activity.png)

*The audit event records the action, success result, and initiating user.*

### Figure 5b — Audit target

![Audit target identifying James Taylor](../screenshots/phase-08-rbac-auditing/05b-audit-log-target.png)

*The supplied Target tab identifies the user affected by the reset.*

### Figure 6a — CA001 sign-in evaluation

![Sarah Johnson's successful CA001 Conditional Access evaluation](../screenshots/phase-08-rbac-auditing/06a-signin-log-validation.png)

*CA001 is enabled and successful, with grant controls satisfied.*

### Figure 6b — CA002 sign-in evaluation

![Sarah Johnson's CA002 evaluation with Browser not matched](../screenshots/phase-08-rbac-auditing/06b-signin-log-validation.png)

*CA002 is enabled but not applied because the Browser client does not match.*

## Skills demonstrated

- Mapping support and service responsibilities to administrative roles.
- Documenting direct role assignments and their standing-access characteristics.
- Validating a delegated password reset against both interface and audit evidence.
- Verifying access to the Teams administration view.
- Identifying the actor, action, target, and outcome in Microsoft Entra audit details.
- Interpreting Conditional Access Success and Not Applied results in context.
- Separating assigned permissions from tested access and observed actions.

## Lessons learned

1. **Delegate according to responsibilities.** Daniel's support task was completed with Helpdesk Administrator. Alex's service responsibilities were represented by four specific roles instead of Global Administrator.
2. **Role assignments and operational tests prove different things.** Alex's role list establishes configuration; his Teams screenshot establishes access to one administration view. Other workloads need their own evidence before their tests can be reported as successful.
3. **Audit both the actor and the target.** The Activity and Target views make the password-reset record understandable and attributable.
4. **Interpret policy results in context.** Not Applied can be expected when the client does not match. Success with satisfied grant controls does not, by itself, identify the authentication method or prove a new prompt.
5. **Least privilege still requires review.** The visible assignments are permanent. Periodic reassessment of who needs each role is a lesson from this design, not an additional control demonstrated by these screenshots.

**Review checkpoint:** Phase 8 is ready for final review. Phases 1–7 are preserved.
