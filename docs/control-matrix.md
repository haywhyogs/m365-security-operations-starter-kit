# Microsoft 365 Security Control Matrix

## Purpose

This matrix ranks five security controls for a business with 100 users,
two administrators, and Microsoft 365 E7 licenses.

The ranking considers risk reduction, likely business impact, implementation
effort, and the ability of a small IT team to maintain each control.

These are proposed priorities for the scenario, not a claim that the
organization has already implemented or tested them.

## Ranked Recommendations

### 1. Enforce Multifactor Authentication (MFA)

**Risk addressed:** Account compromise through stolen or reused credentials.

**Why this ranks first:** Identity is a critical entry point to email,
files, administrative portals, and other organizational resources.

**Implementation approach:**
- Review existing authentication methods and Conditional Access policies.
- Ensure users can register suitable authentication methods.
- Require MFA for all users and stronger, phishing-resistant authentication
  for administrators where supported.
- Pilot the policy, review sign-in results, and then expand enforcement.
- Establish and test account recovery procedures before broad enforcement.

**Validation evidence:**
- Review the effective Conditional Access policy and its assignments.
- Test representative user and administrator sign-ins.
- Confirm that authentication requirements are enforced as intended.

**Tradeoffs:** Additional sign-in steps, registration support, and possible
lockouts. Recovery procedures and carefully controlled emergency access
must be considered.

**Operational owner:** IT administrators.

### 2. Block Legacy Authentication

**Risk addressed:** Authentication through older protocols that cannot
enforce modern authentication protections.

**Why this ranks second:** Legacy access paths can undermine an otherwise
strong authentication strategy.

**Implementation approach:**
- Review sign-in logs for legacy authentication.
- Identify business applications, devices, or clients that depend on it.
- Resolve legitimate dependencies before enforcing a block.
- Apply a Conditional Access policy covering the relevant legacy clients.

**Validation evidence:**
- Confirm that the policy is enabled and targets the intended users
  and resources.
- Review sign-in logs for blocked legacy attempts.
- Test approved modern clients to identify unintended disruption.

**Tradeoffs:** Older mail clients, devices, or applications may stop working.
Some users may require configuration changes or replacement clients.

**Operational owner:** IT administrators, with application owners involved
where necessary.

### 3. Implement Risk-Based Conditional Access

**Risk addressed:** Suspicious sign-ins and compromised accounts that
require additional verification or remediation.

**Why this ranks third:** Risk signals can help the organization respond
to suspicious activity rather than treating every sign-in identically.

**Implementation approach:**
- Review available identity risk signals and current policies.
- Require MFA for elevated sign-in risk.
- Define a suitable remediation process for high user risk.
- Pilot policy behavior and monitor sign-in outcomes before expanding
  enforcement.
- Document how administrators will investigate false positives.

**Validation evidence:**
- Review policy assignments, risk conditions, grant controls, and
  session requirements.
- Use available policy evaluation tools and sign-in logs.
- Confirm that test scenarios produce the intended access decisions.

**Tradeoffs:** False positives can interrupt legitimate access. Risk-based
features depend on licensing, signal availability, and correct policy
configuration.

**Operational owner:** IT administrators.

### 4. Restrict User Consent to Applications

**Risk addressed:** Malicious or overprivileged applications obtaining
access to organizational data through user-granted permissions.

**Why this ranks fourth:** A legitimate user can unintentionally authorize
an application that exposes company information.

**Implementation approach:**
- Review the organization's user-consent settings and existing app grants.
- Disable or appropriately restrict ordinary-user consent.
- Establish a simple application review and approval process.
- Document who reviews requested permissions and how approvals are recorded.

**Validation evidence:**
- Verify the effective user-consent configuration.
- Review application permissions and existing grants.
- Test the approval process using a controlled, non-production scenario
  where available.

**Tradeoffs:** Users may need to wait for IT approval to use new applications.
The approval process must be responsive enough to avoid unnecessary delays.

**Operational owner:** IT administrators, consulting application owners
when business context is needed.

### 5. Secure Microsoft Teams Meetings

**Risk addressed:** Unauthorized meeting access, unwanted presentations,
and exposure of business discussions or information.

**Why this ranks fifth:** Collaboration settings help reduce accidental
disclosure and disruption during internal and external meetings.

**Implementation approach:**
- Review organization-wide meeting policies and relevant exceptions.
- Restrict who can bypass the lobby.
- Set appropriate presenter permissions, limiting presentation rights
  to organizers and co-organizers by default.
- Disable anonymous meeting access where business requirements permit.
- Communicate how external guests should join meetings.

**Validation evidence:**
- Inspect the effective Teams meeting policies.
- Test representative internal, invited-guest, and anonymous-user scenarios
  where permitted.
- Confirm that lobby and presenter behavior matches the intended policy.

**Tradeoffs:** Stricter meeting controls may add friction for customers,
partners, and other external participants. Exceptions should be justified
and reviewed.

**Operational owner:** IT administrators, with business meeting organizers
responsible for day-to-day use.

## Rollout Principles

For all five controls:

1. Establish the current configuration and business dependencies.
2. Define the expected outcome and how it will be verified.
3. Pilot changes where practical before broad enforcement.
4. Communicate user impact and prepare support procedures.
5. Review evidence after rollout and document unresolved issues.
6. Reassess controls periodically and after significant changes.

Changes should follow an approved process. Recovery and rollback options
must be considered before enforcement, especially for policies that can
affect administrator access.

## Scope and Limitations

This matrix is a planning document, not an automated security assessment.
The recommendations must be validated against the organization's actual
configuration, licensing, business requirements, and available features.

A successful configuration check does not by itself prove that an
organization is secure or that every possible attack is prevented.
