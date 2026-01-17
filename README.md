# 🔐 AWS IAM Multi-User Security Lab (Least Privilege RBAC + MFA + CloudTrail)

This lab simulates a real-world AWS environment with multiple identities and security controls. It implements **role-based access control (RBAC)** using IAM groups and policies, enforces **least privilege**, secures console access with **MFA**, and validates monitoring/auditability using **AWS CloudTrail**.

The objective is to demonstrate that restricted actions are denied by IAM policy enforcement and that security personnel can investigate attempted actions using CloudTrail event logs.

---

## 🧠 What This Lab Demonstrates

- Identity and Access Management design using **IAM Users, Groups, and Policies**
- **Separation of duties** (Admin vs Analyst vs Intern)
- Enforcement of **least privilege access**
- **Multi-factor authentication (MFA)** for console login protection
- Security investigation using **AWS CloudTrail** event history
- Validation of controls through real denied actions (`AccessDenied`)

---

## 🏗️ Environment Overview

### IAM Identities

| Role | IAM User | Access Model |
|------|----------|--------------|
| Administrator | `lab-admin` | Full access to manage identities, permissions, and configuration |
| Security Analyst | `lab-analyst` | Audit/read visibility to investigate activity (no admin changes) |
| Intern / Restricted User | `lab-intern` | Limited permissions; blocked from privileged actions |

### Access Strategy
- Permissions are assigned primarily through **IAM Groups**
- AWS-managed policies are used where appropriate
- A restricted permission model is applied to the intern user to prevent high-impact actions

---

## 🔐 Security Controls Implemented

### ✅ Role-Based Access Control (RBAC)
IAM groups were created to represent organizational roles:
- Admin Group: full access for configuration and access management
- Analyst Group: audit-focused visibility for investigation tasks
- Intern Group: limited scope access designed for observation only

### ✅ MFA Enforcement
MFA was enabled on AWS console users to reduce risk of unauthorized access due to password compromise.

### ✅ Least Privilege Access Design
Restricted identities were prevented from performing write/admin actions across AWS services, including S3 and IAM.

---

## 🧪 Control Validation (Testing)

A restricted user (`lab-intern`) attempted an unauthorized action that requires write permissions:

- **Event Name:** `CreateBucket`
- **AWS Service:** Amazon S3
- **Event Source:** `s3.amazonaws.com`
- **Result:** `AccessDenied`

This confirms IAM policy enforcement is functioning as intended.

---

## 🕵️ Audit Logging & Investigation (CloudTrail)

### Logging
AWS CloudTrail was enabled to record management activity across the account.

### Investigation Workflow (SOC-style)
While signed in as `lab-analyst`, CloudTrail **Event history** was reviewed to investigate restricted user activity.

Lookup attribute used:
- `User name = lab-intern`

This allowed tracking attempted actions, timestamps, source IP details, and authorization failures.

---

## 📌 Key Outcome

This lab proves:
- IAM policies successfully enforce least privilege controls
- Unauthorized actions are blocked and logged
- A security analyst can investigate user behavior using centralized audit logs

---

## 💡 Skills Demonstrated

- AWS IAM (Users, Groups, Policies)
- RBAC and separation of duties design
- Least privilege access enforcement
- MFA authentication controls
- CloudTrail event investigation & auditing
- Security monitoring mindset (SOC fundamentals)

---

## ✅ Resume Bullet Points (Ready-to-use)

- Implemented role-based access control (RBAC) in AWS using IAM users/groups/policies to enforce least-privilege access and separation of duties
- Secured AWS Management Console logins using multi-factor authentication (MFA) to reduce risk of credential-based compromise
- Enabled and analyzed AWS CloudTrail audit logs to investigate restricted user activity and validate enforcement through `AccessDenied` events (e.g., S3 `CreateBucket`)

---

## 🚀 Future Improvements

- Send CloudTrail logs to CloudWatch Logs and create alerting rules for repeated authorization failures
- Create IAM policy conditions requiring MFA (`aws:MultiFactorAuthPresent`) for sensitive actions
- Add resource-level restrictions using ARNs instead of wildcard resources where possible
- Build a basic incident response playbook for unauthorized activity detection
