# Microsoft 365 Security Validation Checklist

Use this checklist after each rollout phase. Record results and investigate failures before enforcing changes broadly.

## 1. Multifactor Authentication (MFA)
- [ ] Confirm MFA is required for all users.
- [ ] Confirm administrators use strong authentication.
- [ ] Test sign-in with a pilot account.

## 2. Legacy Authentication
- [ ] Confirm the Conditional Access policy blocks legacy authentication.
- [ ] Review sign-in logs for blocked attempts.
- [ ] Investigate legitimate applications that may depend on legacy authentication.

## 3. Risk-Based Conditional Access
- [ ] Confirm sign-in risk and user risk policies are enabled.
- [ ] Verify configured remediation requirements.
- [ ] Review Identity Protection detections and policy outcomes.

## 4. User Consent and App Permissions
- [ ] Confirm user consent is restricted according to policy.
- [ ] Test the application consent and approval process.
- [ ] Review existing app permissions and remove unnecessary access.

## 5. Microsoft Teams Meetings
- [ ] Confirm anonymous meeting access follows organizational policy.
- [ ] Confirm default presenter permissions are restricted.
- [ ] Test meeting access with an authorized user and an external participant.

## 6. Operational Readiness
- [ ] Review Conditional Access and sign-in logs.
- [ ] Confirm emergency access and recovery procedures.
- [ ] Document exceptions, owners, and remediation actions.
- [ ] Record validation results and the date reviewed.

## Recording Results

For each check, record:
- **Status:** Pass / Fail / Not tested
- **Evidence:** Relevant policy, log, or test result
- **Owner:** Person responsible
- **Follow-up:** Required action and target date

> A configured policy is not proof of effective protection. Validate actual behavior and document the evidence.
