# Microsoft 365 Security Validation Checklist

Use this checklist after each rollout phase. A configured policy is not
proof of effective protection: validate actual behavior and record the
evidence. Mark anything not run as **Not Tested** rather than assuming it
passed.

## 0. Emergency Access

- [ ] Both emergency accounts exist, are cloud-only, and hold Global Administrator rights.
- [ ] Both are excluded from every Conditional Access policy.
- [ ] A sign-in alert fires for either account.
- [ ] Each account has been tested through the documented recovery path.

**Expected evidence:** Conditional Access exclusion lists showing both
accounts; the alert configuration; a dated test sign-in record.

**If it fails:** do not proceed with enforcement. Fix emergency access
first — it is the rollback path for everything else.

## 1. Multifactor Authentication (MFA)

- [ ] MFA is required for all users across all resources.
- [ ] Administrators are required to use phishing-resistant methods (passkeys/FIDO2, Windows Hello for Business, or certificate-based authentication).
- [ ] Emergency accounts are excluded.
- [ ] Authentication method registration coverage is sufficient for the enforced population.
- [ ] Test sign-ins with a registered pilot user, an unregistered user, and an administrator.

**Expected evidence:** effective Conditional Access policy view; sign-in
records showing the MFA claim; registration coverage report showing the
share of users who are MFA-capable.

**If it fails:** set the policy back to report-only, identify the failing
population from the sign-in logs, register methods or issue temporary
access passes, then re-enforce. Do not add permanent user exclusions.

## 2. Legacy Authentication

- [ ] The Conditional Access policy blocks legacy authentication protocols for all users.
- [ ] Sign-in logs show blocked legacy attempts.
- [ ] Every legitimate legacy dependency identified in inventory has been resolved or formally excepted with an expiry date.

**Expected evidence:** policy configuration; sign-in logs filtered to
blocked legacy clients, with client names and counts.

**If it fails:** disable the block policy, resolve the specific client or
application dependency (modern authentication settings or a replacement
client), and re-enforce. Keep the policy; do not delete it.

## 3. Risk-Based Conditional Access

- [ ] Sign-in risk policy requires MFA for medium and high risk sign-ins.
- [ ] User risk policy remediates high-risk accounts through password change or risk remediation.
- [ ] Administrators understand how to investigate and clear false positives.
- [ ] Policy evaluation (What If) and real sign-in tests produce the intended decisions.

**Expected evidence:** policy definitions showing risk conditions and
grant controls; Identity Protection risk events and their policy outcomes.

**Note:** sign-in risk flags a *sign-in attempt*; user risk flags the
*account itself*. They are different signals and need different responses —
challenging the first, remediating the second.

**If it fails:** a false positive is cleared by completing the required
remediation for the affected user; a policy misconfiguration is rolled back
to report-only and corrected.

## 4. User Consent and App Permissions

- [ ] Users cannot consent to applications by default; requests route to an admin approval process.
- [ ] Existing consent grants have been reviewed and unnecessary ones revoked.
- [ ] The approval process has been tested end to end.

**Expected evidence:** the effective user-consent setting; a tested
approval request; the reviewed application permission list.

**If it fails:** the previous consent policy assignment is the rollback.
Do not leave the tenant without any consent governance while debugging.

## 5. Microsoft Teams Meetings

- [ ] Only invited participants are admitted automatically; others wait in the lobby.
- [ ] Presenter rights are limited to organizers and co-organizers by default.
- [ ] Anonymous join is disabled where business requirements permit.
- [ ] Tested with an internal user, an invited external guest, and (where permitted) an anonymous user.

**Expected evidence:** effective Teams meeting policy values; test meeting
notes covering lobby and presenter behavior for each participant type.

**If it fails:** restore the recorded original policy values and correct
the setting. Teams changes have no authentication lockout risk, so rollback
is low urgency — but unverified presenter settings can disrupt live
meetings, so test before business-critical events.

## 6. Operational Readiness

- [ ] Every temporary exclusion has an owner and an expiry date.
- [ ] The rollback operator and procedure are documented for each enforced control.
- [ ] Validation results, dates, and owners are recorded.
- [ ] The monthly review cadence has a named owner.

## Recording Results

For each check, record:

- **Status:** Pass / Fail / Not Tested
- **Evidence:** Relevant policy, log, or test result
- **Owner:** Person responsible
- **Follow-up:** Required action and target date

> A configured policy is not proof of effective protection. Validate actual
> behavior and document the evidence.
