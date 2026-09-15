# Phase 1 — Identity and user provisioning

[Back to project overview](../README.md)

## Business requirement

For the Northstar Consulting lab scenario, the identity foundation supports employees accessing Microsoft 365 with individual organizational accounts. This phase documents the user directory that underpins the later collaboration and security phases.

## Implementation evidenced

The supplied Microsoft Entra user-list screenshot shows eight accounts using the `nyashajiri.com` user principal name (UPN) suffix. Each displayed account is a **Member**, with **On-premises sync: No**.

| Display name | User principal name |
| --- | --- |
| Alex Morgan | alex.morgan@nyashajiri.com |
| Daniel Reed | daniel.reed@nyashajiri.com |
| David Wilson | david.wilson@nyashajiri.com |
| Emma Brown | emma.brown@nyashajiri.com |
| Grace Miller | grace.miller@nyashajiri.com |
| James Taylor | james.taylor@nyashajiri.com |
| Melissa Grant | melissa.grant@nyashajiri.com |
| Sarah Johnson | sarah.johnson@nyashajiri.com |

The displayed UPNs follow a consistent `firstname.lastname` pattern. The screenshot establishes the resulting directory state; it does not establish whether these accounts were newly created, adapted from demo users, or provisioned through a bulk process. Eight accounts are visible; this is not a claim about the tenant's total user count.

### User profile and licensing example: Alex Morgan

The additional profile and licensing captures establish the following settings for Alex Morgan only:

| Setting | Observed value |
| --- | --- |
| Department | IT |
| Job title | IT Administrator |
| Account enabled | Yes |
| Usage location | United States |
| License | Microsoft 365 E5 Developer (product label is truncated in the capture) |
| License state | Active |
| Enabled services | 78/78 |
| Assignment path | Direct |

The job title is a profile attribute, not evidence of an assigned administrator role. The license screen shows the assignment state, not the process used to assign it. Enabled services do not by themselves prove successful access to each service.

## Evidence

![Microsoft Entra user list showing eight Northstar lab accounts](../screenshots/phase-01/entra-user-list.png)

*Figure 1. Supplied user-list capture: display names, UPNs, Member user type, and no on-premises synchronization for the eight displayed accounts.*

![Alex Morgan profile configuration](../screenshots/phase-01/02-user-profile-configuration.png)

*Figure 2. Alex Morgan's profile shows the IT department, IT Administrator job title, enabled account, and United States usage location.*

![Alex Morgan license assignment](../screenshots/phase-01/03-user-license-assignment.png)

*Figure 3. Alex Morgan's license displays Active, 78/78 enabled services, and Direct assignment.*

## Validation and testing

The following is a review of the supplied evidence, not a claim that additional live tenant tests were performed.

| Check | Evidence-supported result | Limit |
| --- | --- | --- |
| Accounts present in the directory | Eight named accounts are visible | Does not prove account creation method |
| UPN consistency | All eight use firstname.lastname@nyashajiri.com | Does not prove email delivery or mailbox readiness |
| User type | All eight display Member | Does not establish administrative roles |
| Synchronization status | All eight display No for on-premises synchronization | Does not establish the tenant's broader identity architecture |
| License assignment | Alex Morgan: active Microsoft 365 E5 Developer license, 78/78 enabled services, Direct assignment | Other users' licenses and actual service access are not evidenced |
| Account enabled status | Alex Morgan: Yes | Successful sign-in is not established; other users' status is not shown |
| Department, job title and usage location | Alex Morgan: IT, IT Administrator, United States | These values are not established for other users |

## Troubleshooting

No Phase 1 incident, diagnostic steps, or resolution has been supplied for this case study. No troubleshooting outcome is claimed. Any later addition should record the actual symptom, checks performed, change made, and retest result.

## Skills demonstrated by the evidence

- **Identity administration:** maintaining a lab directory containing organizational Member accounts.
- **Account naming consistency:** using a consistent UPN pattern across the displayed accounts.
- **Directory inspection:** distinguishing user type and synchronization status when reviewing identities.
- **User profile administration:** documenting Alex Morgan's department, job title, account status, and usage location.
- **License review:** identifying Alex Morgan's active license, enabled services count, and direct assignment path.
- **Technical documentation:** separating observable configuration from tests or outcomes that have not been evidenced.

These activities relate to entry-level support work such as reviewing account records during onboarding and gathering evidence for access issues. Alex Morgan's license assignment is evidenced; successful sign-in and end-to-end onboarding remain unverified.

## Evidence needed to complete the implementation narrative

- Whether the accounts were created individually, imported, or adapted from existing demo users.
- Any additional user-property or license evidence needed to describe accounts beyond Alex Morgan.
- Tests actually performed, with their observed results.
- Any Phase 1 issue encountered and its resolution, or confirmation that no issue occurred.

**Review checkpoint:** Phase 1 documentation only. Phase 2 has not been documented.
