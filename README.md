# Microsoft 365 Security Operations Starter Kit

**A practical security hardening and validation playbook for small and medium-sized businesses.**

## The Problem

Small businesses often have limited IT resources but face the same identity, access, and collaboration risks as larger organizations. Security controls are only part of the solution: they must also be deployed safely, validated, and maintained.

This project explores how a business with 100 users, two administrators, and Microsoft 365 E7 licenses can prioritize security improvements without creating unnecessary operational overhead.

## Project Goals

- Rank security controls according to risk reduction and business impact.
- Define a realistic rollout plan for a two-person IT team.
- Describe how to validate that each control is configured as intended.
- Identify operational tradeoffs, failure scenarios, and recovery considerations.
- Apply DevOps principles such as repeatability, change control, and automated documentation checks.

## Five Security Priorities

| Rank | Security control | Primary risk addressed |
|---|---|---|
| 1 | Enforce multifactor authentication (MFA) | Account compromise through stolen credentials |
| 2 | Block legacy authentication | Authentication through outdated protocols that bypass modern protections |
| 3 | Implement risk-based Conditional Access | Suspicious sign-ins and compromised user accounts |
| 4 | Restrict user consent to applications | Malicious or overprivileged applications accessing organizational data |
| 5 | Secure Microsoft Teams meetings | Unauthorized access to meetings, presentations, and business discussions |

## Engineering Approach


For each recommendation, the playbook will document:

1. **Risk:** What could go wrong, and why does it matter?
2. **Implementation:** How can a small IT team deploy the control safely?
3. **Validation:** What configuration evidence or test demonstrates that it works?
4. **Tradeoffs:** What usability, compatibility, or support costs might arise?
5. **Maintenance:** How should the control be reviewed over time?

The proposed workflow follows a prepare, pilot, enforce, validate, and review cycle. 

## Repository Contents

- `docs/control-matrix.md` — Ranked controls, risks, rationale, and tradeoffs.
- `docs/rollout-plan.md` — Phased implementation plan for a two-administrator team.
- `docs/validation-checklist.md` — Validation steps and expected evidence.
- `.github/workflows/docs-check.yml` — Automated documentation checks.

## Project Scope

This repository is a security planning and validation framework. It does not deploy changes to a Microsoft 365 tenant, and its documentation checks do not independently verify tenant security.

Any validation results will be distinguished from proposed tests and recommendations. No credentials, tenant secrets, or raw lab assessment artifacts belong in this public repository.

## Background

This project was developed as part of Microsoft's Defend the Tenant Challenge. Phase 1 involved configuring and assessing ten Microsoft 365 security controls in a lab environment. Phase 2 applies those lessons to a small-business security scenario.

## Intended Outcome

A concise, reusable resource that helps a small IT team make informed security decisions, implement controls responsibly, and verify outcomes rather than relying on configuration assumptions alone.
