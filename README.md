# WindowsEnterpriseLab
This project demonstrates the deployment and administration of a small Windows enterprise environment using Oracle VirtualBox. The lab simulates a business network by implementing Active Directory Domain Services (AD DS), centralized authentication, Group Policy, file sharing, role-based access control (RBAC), and Windows security auditing.

The objective of this project was to gain hands-on experience with Windows Server administration while applying identity and access management concepts commonly used in enterprise IT and cybersecurity environments.

---

## Objectives

* Build a virtual Windows enterprise network
* Configure Active Directory Domain Services
* Centralize authentication using a Windows domain
* Organize users and computers with Organizational Units (OUs)
* Implement Role-Based Access Control (RBAC)
* Configure Group Policy
* Create secure shared folders using NTFS permissions
* Configure Windows auditing and review security logs in Event Viewer

---

## Lab Environment

### Virtual Machines

| Machine  | Operating System      | Purpose                                    |
| -------- | --------------------- | ------------------------------------------ |
| DC01     | Windows Server 2022   | Domain Controller, DNS Server, File Server |
| CLIENT01 | Windows 11 Enterprise | Domain-joined workstation                  |

---

### Network

* VirtualBox Internal Network
* Static IP addressing
* Isolated lab environment

Example network configuration:

| Device   | IP Address    |
| -------- | ------------- |
| DC01     | 192.168.10.10 |
| CLIENT01 | 192.168.10.20 |

Full network diagram:
                Internet (Optional)
                      │
               ───────────────
                      │
                 VirtualBox
               Internal Network
                      │
        ┌─────────────┴─────────────┐
        │                           │
+--------------------+     +---------------------+
| DC01               |     | CLIENT01            |
| Windows Server     |     | Windows 11          |
| Active Directory   |     | Domain Joined       |
| DNS                |     | Alice / Bob Login   |
| File Shares        |     +---------------------+
+--------------------+

---

## Active Directory Configuration

Created a new Active Directory forest and domain:

```text
lab.local
```

Organizational Unit structure:

```text
Lab
├── Users
├── Groups
├── Computers
```

Created domain users:

* `shells1` (Finance)
* `shells2` (Engineering)

Created security groups:

* Finance
* Engineering

Assigned users to their respective security groups to implement Role-Based Access Control (RBAC).

---

## Domain Join

CLIENT01 was joined to the Active Directory domain.

Authentication is centrally managed by the Domain Controller instead of using local Windows accounts.

---

## Group Policy

Configured a Group Policy Object (GPO) for domain workstations.

Example policy:

* Legal logon message displayed before user authentication

This demonstrates centralized policy management across domain-joined systems.

---

## File Sharing and Access Control

Created shared folders:

```text
C:\Shares
├── Public
├── Finance
└── Engineering
```

Configured both Share Permissions and NTFS permissions.

Permissions were assigned using Active Directory security groups rather than individual user accounts.

| Folder      | Finance   | Engineering |
| ----------- | --------- | ----------- |
| Public      | Read      | Read        |
| Finance     | Modify    | No Access   |
| Engineering | No Access | Modify      |

This demonstrates the principle of Least Privilege.

---

## Security Auditing

Configured Windows auditing to monitor security-related activity.

Examples include:

* Successful logon events
* File access events
* Security log review using Event Viewer

This demonstrates how Windows administrators can monitor authentication and access attempts.

---

## Technologies Used

* Oracle VirtualBox
* Windows Server 2022
* Windows 11 Enterprise
* Active Directory Domain Services
* DNS
* Group Policy
* NTFS Permissions
* Shared Folders
* Event Viewer
* Windows Security Auditing

---

## Skills Demonstrated

* Windows Server Administration
* Active Directory Management
* Identity and Access Management (IAM)
* Role-Based Access Control (RBAC)
* Group Policy Management
* Windows Networking
* File Share Administration
* Security Auditing
* Authentication and Authorization
* Least Privilege
* Virtualization

---

## Screenshots

Included screenshots:

* Active Directory Users and Computers
* Organizational Units
* User Accounts
* Security Groups
* Shared Folder Permissions
* Event Viewer Security Log

---

## What I Learned

This project provided practical experience administering a Windows enterprise environment. I learned how Active Directory centralizes authentication, how security groups simplify permission management, how Group Policy applies configuration across domain-joined computers, and how NTFS permissions and auditing work together to secure and monitor access to shared resources.

Building the environment also improved my practical understanding of enterprise identity management and reinforced cybersecurity concepts such as authentication, authorization, least privilege, and audit logging. All things I learned while studying for the CompTIA Security+ exam.

---

## Future Improvements

Possible future enhancements include:

* Add a second domain-joined workstation
* Configure DHCP to automatically assign IP addresses
* Deploy Windows Server Update Services (WSUS)
* Integrate a Security Information and Event Management (SIEM) platform for consolidated security logging
* Add PowerShell automation for user provisioning
* Expand the environment with additional servers and organizational units
