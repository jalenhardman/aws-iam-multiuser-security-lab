🔐 AWS IAM Multi-User Security Lab (RBAC + MFA + CloudTrail)

This project simulates a real AWS organization by creating multiple IAM users with different roles and enforcing **least privilege** permissions using IAM groups and policies. Login security is strengthened with **MFA**, and user activity is monitored using **AWS CloudTrail**.

The goal is to prove that restricted users are blocked from performing unauthorized actions and that security analysts can investigate those actions through audit logs.

---

## 🎯 Objectives

- Build a multi-user AWS IAM environment using **role-based access control (RBAC)**
- Secure logins using **Multi-Factor Authentication (MFA)**
- Enforce **least privilege** permissions for restricted users
- Enable **CloudTrail** logging for audit visibility
- Generate `AccessDenied` events and verify them in CloudTrail

---

## 🏗️ Lab Setup

### IAM Users

| Role | IAM User | Description |
|------|----------|-------------|
| Admin | `lab-admin` | Full admin access for setup and access management |
| Security Analyst | `lab-analyst` | Audit visibility (investigates CloudTrail events) |
| Intern | `lab-intern` | Restricted permissions (blocked from write actions) |

---

## 🔑 Security Controls Implemented

### ✅ Strong Access Management
- IAM groups used for permission assignment
- AWS-managed policies used where appropriate
- Custom policy created for intern restrictions

### ✅ MFA Secured Logins
MFA was enabled to simulate real enterprise authentication protections and prevent unauthorized access if credentials are compromised.

### ✅ Least Privilege (Intern Restrictions)
The intern account is restricted from performing privileged actions such as:
- Creating S3 buckets
- Modifying IAM resources
- Making changes to AWS services

---

## 🧪 Testing & Validation

### Unauthorized Action Attempt (Intern)
While signed in as `lab-intern`, a restricted action was attempted:

- **Event Name:** `CreateBucket`
- **Event Source:** `s3.amazonaws.com`
- **Result:** `AccessDenied`

This confirms permissions were correctly restricted through IAM policy enforcement.

---

## 🕵️ Audit Investigation (CloudTrail)

While signed in as `lab-analyst`, CloudTrail **Event history** was used to investigate intern activity.

Lookup attribute used:
- `User name = lab-intern`

This demonstrates a real-world SOC-style workflow:

1. User attempts action
2. AWS blocks action using IAM policy enforcement
3. CloudTrail logs the event
4. Security analyst investigates and verifies the event details

---

## 📸 Evidence

Screenshots are included under the `evidence/` folder and show:

- CloudTrail event list filtered by `lab-intern`
- Detailed CloudTrail event showing:
  - `eventName: CreateBucket`
  - `errorCode: AccessDenied`

---

## 💡 Skills Demonstrated

- AWS IAM (Users, Groups, Policies)
- Role-Based Access Control (RBAC)
- Least Privilege permissions design
- MFA security controls
- AWS CloudTrail auditing & investigation
- Security monitoring mindset (SOC fundamentals)

---

## ✅ Resume Bullet Points

- Built a multi-user AWS lab using IAM users/groups to enforce **role-based access control (RBAC)** and **least-privilege permissions**
- Secured AWS console access using **MFA**, and validated permission boundaries through blocked unauthorized actions resulting in `AccessDenied`
- Enabled and analyzed **AWS CloudTrail** events to investigate user activity and verify security control enforcement

---

## 🚀 Future Improvements

- Integrate CloudTrail logs with CloudWatch Logs
- Create alerts for `AccessDenied` events
- Add an IAM policy requiring MFA for sensitive actions
- Restrict policies by specific resources (ARN-level restriction)
