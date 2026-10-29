# Evidence and Limitations

## Purpose

This document defines how security recommendations are validated and how results are reported. The repository is a planning and validation starter kit, not an automated tenant-hardening solution.

## Evidence to Collect

| Control | Suggested Evidence |
|---|---|
| MFA | Conditional Access configuration and sign-in test results |
| Legacy authentication | Policy configuration and sign-in logs |
| Risk-based access | Identity Protection policy settings and risk-event results |
| App consent | User consent settings and application approval test |
| Teams meetings | Meeting policies and tests using representative accounts |

## Validation Requirements

- Record each check as Pass, Fail, or Not Tested.
- Link results to relevant configuration, logs, or test evidence.
- Record the validation date, responsible owner, and follow-up actions.
- Redact usernames, tenant identifiers, tokens, and other sensitive information before publishing evidence.
- Investigate failures before expanding enforcement beyond the pilot group.

## Limitations

- Documentation does not prove that a control is configured or working.
- The GitHub Actions workflow checks that required documentation files exist and are non-empty; it does not assess Microsoft 365 security.
- No live tenant configuration, remediation, or continuous monitoring is performed by this repository.
- Available policies and capabilities depend on licensing, tenant configuration, and organizational requirements.
- Validation results apply only to the environment and time in which the tests were performed.

## Reporting Standard

Only claim a control is effective when supporting evidence demonstrates the expected behavior. Mark untested controls as **Not Tested**, document exceptions, and identify remediation owners.

