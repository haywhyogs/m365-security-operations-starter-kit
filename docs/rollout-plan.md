# Microsoft 365 Security Rollout Plan

The control ranking answers *what reduces the most risk*. This plan answers a
different question: *in what order can a two-person team switch these controls
on without breaking the business or locking themselves out*. Deployment order
follows technical dependency and lockout risk, not rank order.

## Stage 0: Emergency Access (Prerequisite — Before Any Policy Change)

Nothing in this plan is safe without this stage.

- Create **two** cloud-only emergency access ("break-glass") accounts.
- Give each permanent Global Administrator rights, used only for recovery.
- Exclude both accounts explicitly from every Conditional Access policy.
- Use an authentication method that does not depend on the systems being
  changed (for example, a FIDO2 security key), stored under controlled
  procedures.
- Configure an alert on every sign-in to either account.
- Test both accounts through the documented recovery path.

A policy that accidentally blocks all administrators is recoverable only if
one of these accounts still works. If a faulty policy is ever triggered, the
response is to sign in with an emergency account and set the policy state to
**disabled** — never delete the policy, because the definition and its
sign-in evidence are needed to diagnose the failure.

## Stage 1: Inventory and Readiness

- Record all existing Conditional Access policies, conditions, grant
  controls, and exclusions.
- Measure authentication method registration: identify users who cannot yet
  satisfy an MFA requirement.
- Review sign-in logs for legacy authentication usage and identify any
  business application or device that depends on it.
- Review existing application consent grants and the current user-consent
  setting.
- Record the current Teams meeting policy values before changing any of them.
- Review administrative role assignments for unnecessary standing access.

Assemble a **pilot group** that represents the real population: a standard
cloud-only user, a synchronized user, an administrator, a passwordless user,
every critical client type, and every operational region.

## Stage 2: Dry Run (Report-Only)

Conditional Access policies are first created in **report-only** mode. In
this mode the policy evaluates each sign-in and logs what it *would* have
done, without blocking anyone. This is the equivalent of running a change in
dry-run mode before applying it: the decision logic is exercised against real
traffic, and the blast radius is zero.

Keep every policy in report-only for at least one full business cycle, then
review the sign-in logs filtered by policy and report-only result. Check
interactive *and* non-interactive sign-ins — a successful interactive pilot
does not prove that background clients, mail clients, or service accounts
are compatible.

## Stage 3: Pilot Enforcement

Enable each policy for the pilot group only. Observe a complete business
cycle. Record every failure, classify it (user not registered, incompatible
client, false positive, legitimate dependency), and resolve it before
expanding.

## Stage 4: Full Enforcement, in Dependency Order

Enable each change during a monitored change window, one stage at a time,
with the rollback operator identified in advance.

1. **Block legacy authentication.** Close the bypass paths first. Legacy
   protocols cannot perform MFA, so leaving them open undermines every
   authentication control that follows.
2. **Require MFA for all users.** Enforced only after registration coverage
   is sufficient and legacy paths are closed.
3. **Risk-based Conditional Access.** Sign-in risk challenges suspicious
   sign-in attempts; user risk remediation acts on accounts that are likely
   compromised. Both depend on MFA and password reset working already, so
   they come after stage 2.
4. **Restrict application consent.** An authorization-layer change with no
   authentication lockout risk; it can proceed once identity controls are
   stable.
5. **Teams meeting controls.** Tenant-wide collaboration settings with no
   authentication lockout risk. They can be applied in any window, but they
   are placed last because their operational risk is the lowest and they do
   not block the identity work.

Staged rollout for larger populations: clone the policy for a wave group,
expand in controlled waves, enable the all-user policy last, and retire the
wave policies. Avoid overlapping wave policies that cannot be
troubleshooted.

## Stage 5: Validation

Run `docs/validation-checklist.md` against the enforced configuration. Use
the Conditional Access **What If** tool before real sign-in tests, then
perform representative sign-in tests for each population: registered user,
unregistered user, administrator, emergency account, legacy client, and
external meeting participant. Record evidence and the validation date.

## Stage 6: Ongoing Review

- **Monthly:** review sign-in risk events, new application consent grants,
  administrative role assignments, and policy changes.
- **Quarterly:** test both emergency access accounts, review every temporary
  exclusion for an owner and expiry date, and re-run the validation
  checklist.

## Rollback Procedures

| Change | Rollback action | Evidence to preserve first |
|---|---|---|
| Conditional Access policy | Set state to disabled; keep the policy | Policy definition and failing sign-in records |
| Legacy authentication block | Disable the block policy | List of blocked clients and their owners |
| Consent restriction | Restore the previous grant policy assignment | Original assignment record |
| Teams meeting settings | Restore recorded original property values | Original values captured in Stage 1 |
| Administrative role change | Reassign the previous role assignment | Assignment identifier to restore |

Rollback data is captured *before* enforcement, not during the incident.

## Suggested Timeline (Two Administrators, 100 Users)

| Week | Focus |
|---|---|
| 1 | Stage 0 and 1: emergency access, inventory, pilot group, policies created in report-only |
| 2 | Review report-only results; Stage 3 pilot enforcement for MFA and legacy authentication |
| 3 | Stage 4 full enforcement in dependency order |
| 4 | Stage 5 validation, then hand over to the monthly review cycle |

## Operating Constraints

- Two administrators share implementation and review responsibilities; the
  rollback operator for each change is the *other* administrator.
- Schedule changes to minimize disruption and announce user-facing changes
  in advance.
- Document every exception with an owner and an expiry date; permanent
  exclusions for ordinary users are not acceptable.
- Never rely on a successful configuration check alone as proof of security.
