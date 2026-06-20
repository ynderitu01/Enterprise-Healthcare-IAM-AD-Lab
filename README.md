# Enterprise Healthcare IAM and Active Directory Lab

**Environment:** Windows Server 2022 | Active Directory Domain Services | Microsoft Azure  
**Scope:** 200-user simulated hospital network | 3 clinical departments | HIPAA-compliant

---

## Overview

This lab simulates a real enterprise healthcare IT environment. I built and configured a full Active Directory domain from scratch for a mock hospital network i dont have the screenshoatlantacare.local), covering user provisioning, role-based access control, group policy enforcement, and HIPAA-compliant security baselines.

This is the kind of environment a Healthcare IT Support Specialist or IAM Associate would manage day to day.

---

## Environment Setup

- Windows Server 2022 deployed and promoted to Domain Controller
- Domain: atlantacare.local
- Organizational Units (OUs) structured by department
- 200+ simulated user accounts provisioned

---

## What I Built

### 1. Active Directory Domain Architecture
- Deployed Windows Server and configured Active Directory Domain Services (AD DS)
- Promoted the server to a Domain Controller for the atlantacare.local forest
- Designed a 3-tier OU hierarchy to separate staff by role and department

**Departments configured:**
- Physicians
- Nursing
- Pharmacy

### 2. Role-Based Access Control (RBAC)
- Created security groups for each department with appropriate access levels
- Provisioned individual user accounts with role-specific permissions
- Restricted access to sensitive folders and network shares by group membership
- Configured file sharing permissions to limit PHI access to authorized users only

### 3. Group Policy (GPO) Enforcement
- Enforced password complexity requirements across all OUs
- Set mandatory "User must change password at next logon" for all new accounts
- Configured account lockout policies to meet enterprise security baselines
- Applied desktop and security policies by department

### 4. User Provisioning Workflows
- Built a repeatable process for onboarding new users including account creation, group assignment, and access provisioning
- Simulated bulk onboarding for a new department intake
- Documented offboarding steps including account disabling and access revocation

### 5. HIPAA Compliance Implementation
- Applied MediClear
