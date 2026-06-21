# Enterprise Healthcare IAM & Active Directory Lab

**Platform:** Windows Server 2022 | Active Directory Domain Services | Group Policy  
**Domain:** dationcare.local  
**Scope:** 4 departments | 8 users | 4 security groups | Healthcare-focused security controls

---

## Overview

This lab simulates a real enterprise Healthcare IT environment built from scratch. I deployed and configured a full Active Directory domain for a mock hospital network. The project covers domain controller setup, organizational unit design, user provisioning, role-based access control, group policy enforcement, and department file share permissions.

This is the type of environment a Healthcare IT Support Specialist or IAM Associate manages day to day.

---

## Skills Demonstrated

- Windows Server 2022 installation and configuration
- Active Directory Domain Services (AD DS)
- Domain Controller promotion
- Organizational Unit (OU) design
- User provisioning and account management
- Role-Based Access Control (RBAC)
- Security group management
- Group Policy Object (GPO) creation and linking
- Password and account lockout policy enforcement
- File share permissions
- Healthcare security policy implementation

---

## Part 1 - Windows Server Installation

Deployed Windows Server 2022 in VirtualBox and performed a clean installation. Configured language settings, installation type, and administrator credentials.

![Windows Server Setup](Screenshots/01-windows-server-setup.jpg)

![Install Now](Screenshots/02-install-now.jpg)

![OS Selection](Screenshots/03-os-selection.jpg)

Selected Windows Server 2022 Standard Evaluation with Desktop Experience for full GUI management access.

![Installation Type](Screenshots/04-installation-type.jpg)

![Drive Selection](Screenshots/05-drive-selection%20(1).jpg)

![Admin Password Setup](Screenshots/06-admin-password-setup.jpg)

![Admin Login](Screenshots/07-admin-login.jpg)

![Server Manager Dashboard](Screenshots/08-server-manager-dashboard.jpg)

---

## Part 2 - Active Directory Domain Services Installation

Installed the AD DS role using the Add Roles and Features Wizard. Included all required management tools and Group Policy Management components.

![Add Roles Wizard](Screenshots/09-add-roles-wizard.jpg)

![Installation Type](Screenshots/10-installation-type.jpg)

![Server Selection](Screenshots/11-server-selection.jpg)

![Server Roles](Screenshots/12-server-roles.jpg)

Selected Active Directory Domain Services along with all required features including Group Policy Management, Remote Server Administration Tools, and the Active Directory PowerShell module.

![AD DS Selected](Screenshots/14-ad-ds-selected.jpg)

![AD DS Info](Screenshots/15-ad-ds-info.jpg)

![Confirm Installation](Screenshots/16-confirm-installation.jpg)

![AD DS Installed](Screenshots/17-ad-ds-installed.jpg)

---

## Part 3 - Domain Controller Promotion

Promoted the server to a Domain Controller and created a new forest with dationcare.local as the root domain.

![Post Deployment Config](Screenshots/18-post-deployment-config.jpg)

![Deployment Configuration](Screenshots/19-deployment-configuration.jpg)

![New Forest Dationcare](Screenshots/20-new-forest-dationcare.jpg)

![Domain Controller Options](Screenshots/21-domain-controller-options.jpg)

![DNS Options](Screenshots/22-dns-options.jpg)

DNS delegation warning is expected in a private lab environment. No public parent zone exists for dationcare.local so delegation was not configured.

![NetBIOS Name](Screenshots/23-netbios-name.jpg)

![AD Paths](Screenshots/24-ad-paths.jpg)

![Review Options](Screenshots/25-review-options.jpg)

![Prerequisites Check](Screenshots/26-prerequisites-check.jpg)

All prerequisite checks passed. Server promoted and rebooted automatically as the dationcare.local Domain Controller.

![Domain Controller Success](Screenshots/27-domain-controller-success.png.jpg)

---

## Part 4 - Organizational Unit Design

Opened Active Directory Users and Computers and built a department-based OU structure to organize hospital staff by role.

![Active Directory Users and Computers](Screenshots/28-active-directory-users-computers.png.jpg)

![Physicians OU Created](Screenshots/29-physicians-ou-created.png.jpg)

Created 4 department OUs: Physicians, Nursing, Pharmacy, and Billing.

![All OUs Created](Screenshots/30-all-ous-created.jpg)

---

## Part 5 - User Provisioning

Provisioned 8 user accounts across all 4 departments. All accounts were configured with mandatory password reset at first logon.

![First User Created](Screenshots/31-first-user-created.jpg)

![Physicians Users](Screenshots/32-physicians-users.jpg)

![Nursing Users](Screenshots/33-nursing-users.jpg)

![Pharmacy Users](Screenshots/34-pharmacy-users.jpg)

![Billing Users](Screenshots/35-billing-users.jpg)

**Users provisioned:**

| Department | User | Logon Name |
|---|---|---|
| Physicians | James Carter | jcarter |
| Physicians | Sarah Patel | spatel |
| Nursing | Marcus Williams | mwilliams |
| Nursing | Tanya Roberts | troberts |
| Pharmacy | Linda Chen | lchen |
| Pharmacy | David Kim | dkim |
| Billing | Rachel Moore | rmoore |
| Billing | Kevin Torres | ktorres |

---

## Part 6 - Security Groups and RBAC

Created department security groups and assigned users to enforce Role-Based Access Control across the domain.

![GRP Physicians](Screenshots/36-grp-physicians.jpg)

![GRP Nursing](Screenshots/37-grp-nursing.jpg)

![GRP Pharmacy](Screenshots/38-grp-pharmacy.jpg)

![GRP Billing](Screenshots/39-grp-billing.jpg)

Each user was added to their department security group.

![GRP Physicians Members](Screenshots/40-grp-physicians-members.jpg)

![GRP Pharmacy Members](Screenshots/41-grp-pharmacy-members.jpg)

![GRP Nursing Members](Screenshots/42-grp-nursing-members.jpg)

![GRP Billing Members](Screenshots/43-grp-billing-members.jpg)

---

## Part 7 - Group Policy Configuration

Created the DATIONCARE-Password-Policy GPO to enforce HIPAA-grade password and account lockout requirements across the domain.

![Group Policy Management](Screenshots/44-group-policy-management.jpg)

![GPO Domain Expanded](Screenshots/45-gpo-domain-expanded.jpg)

![Password Policy GPO Created](Screenshots/46-password-policy-gpo-created.jpg)

![GPO Editor](Screenshots/47-gpo-editor.jpg)

![Password Policy Settings](Screenshots/48-password-policy-settings.jpg)

**Password Policy:**

![Min Password Length](Screenshots/49-min-password-length.jpg)

![Enforce History](Screenshots/51-enforce-history.jpg)

![Max Age](Screenshots/52-max-age.jpg)

![Min Age](Screenshots/54-min-age.jpg)

![Complexity Enabled](Screenshots/55-complexity-enabled.jpg)

![Password Policy Complete](Screenshots/56-password-policy-complete.jpg)

| Setting | Value |
|---|---|
| Minimum password length | 12 characters |
| Password history | 10 passwords remembered |
| Maximum password age | 90 days |
| Minimum password age | 1 day |
| Complexity requirements | Enabled |

**Account Lockout Policy:**

![Account Lockout Policy](Screenshots/57-account-lockout-policy.jpg)

![Lockout Threshold](Screenshots/58-lockout-threshold.jpg)

![Lockout Policy Complete](Screenshots/59-lockout-policy-complete.jpg)

| Setting | Value |
|---|---|
| Lockout threshold | 5 invalid logon attempts |
| Lockout duration | 30 minutes |
| Reset counter after | 30 minutes |

---

## Part 8 - GPO Linked to Domain

Linked the DATIONCARE-Password-Policy GPO to dationcare.local so the policies apply to all users and departments automatically.

![Link GPO](Screenshots/60-link-gpo.jpg)

![GPO Linked](Screenshots/61-gpo-linked.jpg)

---

## Part 9 - File Share Permissions

Created department shared folders under DationCare-Shares and assigned each security group access to their folder only.

![DationCare Shares](Screenshots/62-dationcare-shares.jpg)

![Department Folders](Screenshots/63-department-folder.jpg)

Each security group was given Read permissions to their department folder only. A physician cannot access the Nursing or Billing folders. This enforces RBAC at the file system level.

![Physicians Folder Permissions](Screenshots/64-physicians-folder-permissions.jpg)

![Pharmacy Folder Permissions](Screenshots/65-pharmacy-folder-permissions.jpg)

![Billing Permissions](Screenshots/66-billing-permissions.jpg)

![Nursing Permissions](Screenshots/69-nursing-permissions.jpg)

**Troubleshooting note:** During file share setup, Windows blocked removal of an inherited security group from a subfolder. Fixed this by going into Advanced Security Settings, disabling inheritance, and converting inherited permissions to explicit permissions. This is standard practice when applying granular access controls to subfolders in an AD environment.

---

## Healthcare Security Controls Applied

- Role-based access control limiting PHI access to authorized department groups only
- Password complexity and rotation policies enforced via GPO
- Account lockout after 5 failed attempts to prevent brute force access
- Department file shares restricted to matching security groups
- Mandatory password reset at first logon for all provisioned users

---

## Tools and Technologies

Windows Server 2022, Active Directory Domain Services, Group Policy Management, Active Directory Users and Computers, VirtualBox, DNS, File Share Permissions, MediClear HIPAA Compliance Framework
