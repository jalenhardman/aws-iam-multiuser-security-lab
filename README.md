# 🔐 AWS IAM Multi-User Security Lab (RBAC + MFA + CloudTrail)

This project simulates a real AWS organization by creating multiple IAM users with different roles and enforcing **least privilege** permissions using IAM groups and policies. Login security is strengthened with **MFA**, and user activity is monitored using **AWS CloudTrail**.

The lab proves that restricted users are blocked from performing unauthorized actions and that security analysts can investigate those actions through audit logs.

---

## 🎯 Objectives

- Build a multi-user AWS IAM environment using **role-based access control (RBAC)**
- Secure logins with **Multi-Factor Authentication (MFA)**
- Enforce **least privilege** permissions for restricted users
- Enable **AWS CloudTrail** logging for audit visibility
- Generate `AccessDenied` events and verify them in CloudTrail

---

## 🏗️ Lab Setup

### IAM Users

| Role | IAM User | Purpose |
|------|----------|---------|
| Admin | `lab-admin` | Full access for user/group/policy management |
| Security Analyst | `lab-analyst` | Read-only visibility for auditing and investigation |
| Intern | `lab-intern` | Restricted user with limited permissions |

---

## 🔑 Security Controls Implemented

### ✅ Role-Based Access Control (RBAC)
IAM permissions are assigned using groups/policies to simulate a real enterprise environment.

### ✅ MFA-Secured Logins
MFA was enabled for IAM users to strengthen authentication and protect against credential compromise.

### ✅ Least Privilege Permissions
The intern account was intentionally restricted from performing write actions such as:
- Creating S3 buckets
- Modifying IAM resources
- Making changes to cloud services

---

## 🧪 Testing & Validation

A restricted user (`lab-intern`) attempted an unauthorized action:

- **Event Name:** `CreateBucket`
- **Event Source:** `s3.amazonaws.com`
- **Result:** `AccessDenied`

This confirms IAM permissions were successfully enforced.

---

## 🕵️ Audit Investigation (CloudTrail)

A security analyst user (`lab-analyst`) reviewed AWS CloudTrail **Event history** to investigate intern activity.

Lookup attribute used:
- `User name = lab-intern`

This demonstrates a real SOC-style workflow:
1. User attempts restricted action
2. AWS denies action using IAM policy enforcement
3. CloudTrail records the event
4. Analyst investigates and confirms activity

---

## 💡 Skills Demonstrated

- AWS IAM (Users, Groups, Policies)
- Role-Based Access Control (RBAC)
- Least Privilege access design
- MFA login security
- AWS CloudTrail auditing & investigation

---

## ✅ Resume Bullet Points

- Built a multi-user AWS IAM lab using IAM users/groups to enforce **role-based access control (RBAC)** and **least-privilege permissions**
- Secured AWS console logins with **MFA** and validated policy enforcement through unauthorized actions resulting in `AccessDenied`
- Enabled and analyzed **AWS CloudTrail** event logs to investigate user activity and verify security control effectiveness

---

## 🚀 Future Improvements

- Send CloudTrail logs to CloudWatch Logs
- Create alerts for repeated `AccessDenied` events
- Enforce MFA-required IAM policies for sensitive actions
- Restrict permissions to specific resources (ARN-level restrictions)
