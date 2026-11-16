# Secure AWS Landing Zone & Multi-Account Governance
## Architecture Design — Version 1.0

**Project:** DEPI AWS Security Cloud Computing Capstone  
**Primary Region:** us-east-1 (N. Virginia)  
**Status:** Proposed Architecture — Implementation in Progress

## 1. Project Objective

Design and implement a secure AWS Landing Zone using centralized identity management, network isolation, security monitoring, governance controls, and Infrastructure as Code (IaC).

The target architecture follows AWS multi-account design principles. Implementation will begin in the team's existing AWS account, with multi-account components documented separately until they can be deployed and verified.

## 2. Target Multi-Account Architecture

| Account | Purpose |
|---|---|
| Management | AWS Organizations, account management and cost governance |
| Log Archive | Centralized storage of audit and activity logs |
| Security Tooling | Security monitoring, auditing and threat detection |
| Network | Shared network infrastructure and connectivity |
| Workload | Application resources and isolated development environments |

**Organizational Unit (OU) Structure:**

- Root
  - Security OU: Log Archive, Security Tooling
  - Infrastructure OU: Network
  - Workloads OU: Development / Sandbox

This structure is the **target design**, not a claim that these AWS accounts have already been provisioned.

## 3. Network Architecture

The initial network implementation will be deployed in the existing AWS account.

**VPC Design**

| Component | Planned Configuration |
|---|---|
| AWS Region | us-east-1 |
| VPC CIDR | 10.20.0.0/16 |
| Public Subnet A | 10.20.1.0/24 |
| Public Subnet B | 10.20.2.0/24 |
| Private Subnet A | 10.20.11.0/24 |
| Private Subnet B | 10.20.12.0/24 |
| Availability Zones | Two distinct AZs |

**Network Security**

- An Internet Gateway will support internet connectivity for public subnets.
- Public route tables will contain a default route to the Internet Gateway.
- Private route tables will initially contain local routing only.
- Security Groups will follow the principle of least privilege.
- Network ACLs will provide additional subnet-level controls where required.
- NAT Gateway deployment will be deferred until needed and approved because of its cost.

## 4. Identity and Access Management

**Current implementation:**

- Five dedicated IAM users for team members.
- A shared administrative user group, `DEPI-Admins`.
- Console authentication with individual credentials.
- MFA required as a security hardening task.

**Target architecture:**

- AWS IAM Identity Center for centralized workforce access.
- Role-based permission sets.
- Cross-account access using IAM roles.
- Restricted root account usage and least-privilege permissions.

## 5. Logging and Monitoring

**Planned components:**

- AWS CloudTrail for API activity auditing.
- Amazon CloudWatch for monitoring and alerts.
- AWS Config for resource configuration tracking, subject to availability and cost approval.
- Amazon S3 for secure log storage.
- VPC Flow Logs where required.

In the target multi-account environment, centralized audit records will be stored in the Log Archive account.

## 6. Security Governance

**Planned security controls:**

- Service Control Policies (SCPs) for organizational governance.
- AWS GuardDuty for threat detection.
- AWS Security Hub for consolidated security findings.
- IAM least-privilege and MFA controls.
- Encryption and protection of sensitive resources.

Services requiring a paid plan or additional permissions will not be activated without approval.

## 7. Infrastructure as Code

Infrastructure configurations will be maintained in the GitHub repository.

IaC deliverables will include reusable network and security configurations, documentation, configuration validation, and deployment instructions.

The implementation technology will be selected and recorded by the IaC workstream.

## 8. Implementation Responsibilities

| Team Member | Workstream |
|---|---|
| Youssef Sameh | Organizations, Accounts & Cost Governance |
| Mohamed Fathi | IAM, Identity Center & Cross-Account Access |
| Karim Eldsoky | Secure Network Foundation |
| Amr Mamdouh | Centralized Logging, AWS Config & Audit |
| Mohamed Ashraf | Security Governance, GuardDuty & Security Hub |
| Aya Atef | Infrastructure as Code & Final Integration |

## 9. Implementation Strategy

**Phase 1 — Foundation:** Finalize architecture, configure individual access, design network, and document dependencies.

**Phase 2 — Deployment:** Implement approved network, IAM, logging, and security components in parallel.

**Phase 3 — Integration:** Integrate IaC, validate configurations, and resolve conflicts.

**Phase 4 — Verification:** Capture deployment evidence, document test results, and prepare the final presentation.

## 10. Current Environment and Limitations

The current working environment contains one AWS account with five team IAM users.

IAM users are identities within an AWS account; they are not separate AWS accounts.

Multi-account infrastructure, centralized cross-account logging, SCP enforcement, and other target features must be separately deployed and verified before being described as implemented.

Any AWS Organizations activation or account-plan change requires cost and credit-impact approval.

## 11. Acceptance and Evidence

The project will be evaluated using:

- AWS resource configuration verification.
- Network connectivity and isolation testing.
- IAM permission verification.
- Security logging and monitoring checks.
- IaC validation and reproducibility.
- Screenshots and documented test results.
- Clear distinction between implemented, partially implemented, and design-only components.

**Document status:** Initial architecture baseline. Update this document whenever an implementation decision is finalized or verified.
