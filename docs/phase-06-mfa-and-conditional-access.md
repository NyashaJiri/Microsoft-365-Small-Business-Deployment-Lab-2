# Phase 6 — MFA and Conditional Access

[Back to project overview](../README.md)

## Business requirement

Northstar Consulting needed stronger sign-in protection through multifactor authentication (MFA) and a policy blocking legacy authentication. The deployment also needed an emergency access exception and a testing stage before enforcement to reduce unintended access disruption.

This phase documents CA001 and CA002, the reported Report-only rollout, and the supplied enabled-policy evaluations in Microsoft Entra sign-in logs.

## Implementation evidenced

### Policy overview

The Conditional Access policy list shows two user-created policies, both **On**:

| Policy | Purpose | Current state |
| --- | --- | --- |
| CA001 – Require MFA – All Users | Require MFA for included users | On |
| CA002 - Block Legacy Authentication | Block the configured legacy client-app categories | On |

### CA001 — Require MFA

CA001 requires MFA for all users while excluding the emergency access account. Its supplied summary shows:

| Setting | Displayed configuration |
| --- | --- |
| Included identities | All users |
| Included resources | All resources |
| Excluded identities | 2 users, 0 groups, 0 roles |
| State | On |
| Network | Not configured |
| Client apps | 1 included; category not expanded |

**Exclusion scope:** The emergency-account exclusion is excluded from policy. 

### CA002 — Block legacy authentication

| Setting | Displayed configuration |
| --- | --- |
| Included identities | All users |
| Included resources | All resources |
| Excluded identities | 2 users, 0 groups, 0 roles |
| Requirements for access | Block access |
| Client apps | Exchange active sync clients; Other clients |
| State | On |
| Network | Not configured |

These configured client-app categories define the legacy-authentication policy's scope in the supplied summary. CA002 also has excluded emergency access account.

### Report-only testing before enforcement

I first tested both policies in **Report-only** mode, reviewed their behavior in **Microsoft Entra sign-in logs**, and then enabled them after confirming the expected behavior.

Report-only mode evaluates a policy and records its results without enforcing its access controls. This allows administrators to review policy impact before switching to On. Enabled-policy Success indicates that the policy applied and its requirements were met.
## Validation and testing

### CA001 — Successful application

The CA001 policy evaluation shows:

| Evaluation field | Observed result |
| --- | --- |
| Policy state | Enabled |
| Policy result | Success |
| User | Sarah Johnson — Matched |
| Resource | Microsoft Graph — Matched |
| Client app | Browser; condition displayed as Not configured |
| Grant controls | Satisfied |
| Session controls | Not configured |

**Result:** CA001 applied successfully to the captured evaluation and its grant controls were satisfied. This supports the stated MFA policy's successful evaluation for Sarah. 

### CA002 — Correctly not applied to the browser sign-in

The CA002 evaluation shows:

| Evaluation field | Observed result |
| --- | --- |
| Policy state | Enabled |
| Policy result | Not Applied |
| User | Sarah Johnson — Matched |
| Resource | Microsoft Graph — Matched |
| Client app | Browser — Not matched |
| Device | Unknown — Not evaluated |

**Result:** The user and resource matched, but the Browser client did not match CA002's configured client-app condition. The policy therefore did not apply to the normal modern-browser sign-in as expected.


## Screenshots and evidence

### Figure 1 — Enabled Conditional Access policies

![Enabled Conditional Access policies](../screenshots/phase-06-security/01-conditional-access-policies.png)

*Two user-created policies, CA001 and CA002, both show On.*

### Figure 2 — CA001 policy summary

![CA001 policy summary](../screenshots/phase-06-security/02-ca001-mfa-policy.png)

*CA001 includes all users and all resources, with two unnamed excluded users.*

### Figure 3 — CA001 sign-in evaluation

![CA001 sign-in evaluation](../screenshots/phase-06-security/03-ca001-signin-validation.png)

*Sarah and Microsoft Graph match; CA001 is Enabled, its result is Success, and grant controls are Satisfied.*

### Figure 4 — CA002 legacy-authentication policy

![CA002 legacy-authentication policy](../screenshots/phase-06-security/04-ca002-legacy-auth-policy.png)

*CA002 shows Block access, Exchange active sync clients and Other clients, and two unnamed excluded users.*

### Figure 5 — CA002 browser sign-in evaluation

![CA002 browser sign-in evaluation](../screenshots/phase-06-security/05-ca002-signin-validation.png)

*The Browser client is Not matched, resulting in Not Applied for the enabled CA002 policy.*


## Skills demonstrated

- **Conditional Access administration:** configuring an MFA policy and a legacy-authentication blocking policy.
- **Deployment planning:** testing in Report-only mode before enforcement.
- **Exception awareness:** accounting for the reported emergency-access exclusion while documenting the actual exclusion counts.
- **Sign-in log analysis:** reading assignment matches, client-app conditions, grant controls, and per-policy results.
- **Support troubleshooting:** distinguishing successful enforcement from a policy correctly not applying to a particular client.

