# Phase 7 — Self-Service Password Reset

[Back to project overview](../README.md)

## Business requirement

Northstar Consulting needed users to recover access through Self-Service Password Reset (SSPR), reducing dependence on administrator-assisted resets. Users needed to register authentication information in advance and meet the required verification count before resetting a password.

This phase documents tenant-wide SSPR settings, the reported registration mismatch, and successful reset evidence from both the user experience and Microsoft Entra audit logs.

## Implementation evidenced

### SSPR scope and registration

| Setting | Observed configuration | Evidence |
| --- | --- | --- |
| Self-service password reset enabled | All | Figure 1 |
| Number of methods required to reset | 2 | Figure 2 |
| Require users to register when signing in | Yes | Figure 3 |
| Reconfirm authentication information | Every 180 days | Figure 3 |

The All selection enables SSPR for the tenant's end-user population, including the Northstar lab users. Registration at sign-in prompts users to prepare authentication information. The 180-day value is a reconfirmation interval, not a password-expiration period.

SSPR checks that a user has sufficient registered methods permitted by the applicable policy. A two-method requirement cannot be met with only one eligible method. Registration settings and the user's registered information therefore need to be considered together. [Microsoft Learn: How Microsoft Entra self-service password reset works](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-sspr-howitworks).

### Sarah Johnson's recorded authentication methods

The supplied user Authentication methods view shows:

| Field | Visible value |
| --- | --- |
| Default sign-in method (Preview) | OATH TOTP one-time code |
| Listed method | Email |
| Listed method | Software OATH token |
| Listed method | Passkey |

The screenshot's method details are already obscured and are preserved that way. The case study does not reproduce recovery addresses, token details, or other concealed values.

This is a user-level authentication-method inventory. It does not identify which methods were selected during the successful SSPR flow or establish that every listed method is eligible for SSPR. In particular, the Passkey entry is recorded as a registered authentication method, not claimed as a password-reset verification method. The tenant's complete enabled-method policy is not shown.

## Troubleshooting

### Initial problem

The lab author reports that the test user initially could not reset their password because the tenant required **two authentication methods** while the user had only **one registered method**.

### Diagnostic finding

The mismatch was between the policy requirement and the user's registration readiness. Enabling SSPR for the user population did not, by itself, supply the additional verification method needed for reset.

| Troubleshooting element | Documented finding |
| --- | --- |
| Symptom | Test user initially unable to complete SSPR, as reported by the author |
| Requirement | Two methods required |
| Initial user state | One registered method, as reported by the author |
| Cause identified | Insufficient registered methods to satisfy the reset requirement |
| Current captured state | Two-method setting remains selected; Sarah's method inventory lists Email, Software OATH token, and Passkey |
| Later outcome | Successful reset confirmed by the audit event and user-facing confirmation |

### Resolution evidence and limits

The supplied evidence records the initial cause and a later successful outcome. It does not show the exact corrective sequence, which method was initially registered, which additional method was registered next, or the verification methods used in the completed reset.

The current two-method screenshot is documented as the captured configuration. The successful event is documented separately; the captures do not establish the policy value at the exact instant of that event. No unshown policy change, registration action, or administrator-performed reset is added to the narrative.

**Support lesson:** Compare the required verification count with the user's eligible registered methods when investigating an SSPR failure, then verify the eventual outcome in the audit log.

## Validation and testing

### User-facing success

The reset completion screen displays **Your password has been reset**, with a link to sign in using the new password. This confirms completion of the displayed reset flow. The screenshot does not show a subsequent sign-in or identify the account on that page.

### Microsoft Entra audit evidence

The supplied Audit Log Details capture provides account-specific confirmation:

| Audit field | Displayed value |
| --- | --- |
| Date | September 17, 2026, 1:34 PM — as displayed; timezone not shown |
| Activity Type | Self-service password reset flow activity progress |
| Category | UserManagement |
| Status | success |
| Status reason | User successfully reset password |
| Initiated by — Type | User |
| User Principal Name | sarah.johnson@nyashajiri.com |

The audit event directly supports a successful self-service password reset for Sarah. The status reason is more specific than the general activity name: it explicitly records that the password was reset. No additional audit events, failure codes, or registration events are inferred.

### Validation record

| Check | Result supported by the evidence | Evidence |
| --- | --- | --- |
| SSPR scope | All selected | Figure 1 |
| Reset requirement | Two methods selected | Figure 2 |
| Sign-in registration | Required; 180-day reconfirmation | Figure 3 |
| User registration inventory | Email, Software OATH token, and Passkey listed for Sarah | Figure 4 |
| Account-specific reset outcome | Audit status success; reason confirms successful password reset for Sarah | Figure 5 |
| Reset completion screen | Your password has been reset | Figure 6 |
| Sign-in with the new password | Not captured | No post-reset sign-in evidence supplied |

## Screenshots and evidence

### Figure 1 — SSPR properties

![SSPR properties](../screenshots/phase-07-sspr/01-sspr-properties.png)

*Self-service password reset is enabled for All.*

### Figure 2 — Authentication-method requirement

![Authentication-method requirement](../screenshots/phase-07-sspr/02-sspr-authentication-requirements.png)

*The number of methods required to reset is set to 2.*

### Figure 3 — Sign-in registration policy

![Sign-in registration policy](../screenshots/phase-07-sspr/03-sspr-registration-policy.png)

*Registration at sign-in is set to Yes, with authentication-information reconfirmation after 180 days.*

### Figure 4 — Sarah's authentication-method inventory

![Sarah's authentication-method inventory](../screenshots/phase-07-sspr/04-user-authentication-methods.png)

*Email, Software OATH token, and Passkey are listed; sensitive method details remain obscured as supplied.*

### Figure 5 — Successful SSPR audit event

![Successful SSPR audit event](../screenshots/phase-07-sspr/05-sspr-audit-validation.png)

*Microsoft Entra records success and User successfully reset password for Sarah's user principal name.*

### Figure 6 — User-facing reset confirmation

![User-facing reset confirmation](../screenshots/phase-07-sspr/06-sspr-success.png)

*The completed flow displays Your password has been reset.*

## Skills demonstrated

- **Identity recovery configuration:** reviewing SSPR scope and authentication-method count requirements.
- **Registration administration:** requiring sign-in registration and configuring periodic reconfirmation.
- **Authentication-method review:** inspecting a user's registered methods without disclosing their sensitive details.
- **Troubleshooting:** identifying a mismatch between required methods and initial registration readiness.
- **Audit analysis:** interpreting the activity type, actor, status, and status reason to verify a reset.
- **End-user validation:** documenting the reset completion experience while distinguishing it from a later sign-in test.

These skills support service-desk work involving password recovery, registration assistance, and evidence-based resolution of account-access incidents.

**Review status:** Phase 7 approved. All eight phases are documented; final repository review is pending.
