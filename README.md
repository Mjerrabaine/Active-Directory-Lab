# Active Directory Lab on Microsoft Azure

A hands-on Active Directory infrastructure lab deployed on Microsoft Azure to demonstrate Windows Server administration, Active Directory Domain Services, DNS, Group Policy, domain authentication, security groups, delegated administration, and PowerShell automation.

The environment consists of a Windows Server domain controller and a domain-joined client deployed within the same Azure Virtual Network. The project also includes PowerShell automation for user and group provisioning, bulk user creation from CSV data, Group Policy configuration, and delegated Helpdesk permissions.

---

## Architecture

![Active Directory Lab Architecture](architecture/architecture-diagram.png)

### Environment Overview

The lab is deployed inside an Azure Virtual Network using the `10.0.0.0/24` address space.

| Component | Configuration |
|---|---|
| Cloud Platform | Microsoft Azure |
| Virtual Network | `ADLab-vnet` |
| Network | `10.0.0.0/24` |
| Domain | `lab.local` |
| Domain Controller | `DC01` |
| DC Private IP | `10.0.0.4` |
| Client | `CLIENT01` |
| Operating System | Windows Server 2025 |
| Directory Service | Active Directory Domain Services |
| DNS | Hosted on DC01 |
| Authentication | Active Directory / Kerberos |

---

## Technologies Used

- Microsoft Azure
- Windows Server 2025
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers
- DNS
- Group Policy
- Kerberos
- LDAP
- PowerShell
- CSV-based automation
- Remote Desktop Protocol (RDP)
- Azure Virtual Network

---

## Project Objectives

The main objectives of this lab were to:

- Deploy Windows Server infrastructure in Azure
- Configure a functional Active Directory domain
- Configure DNS for Active Directory
- Design a scalable Organizational Unit structure
- Create and manage domain users
- Implement role-based security groups
- Join a client machine to the domain
- Test domain authentication
- Verify Kerberos group membership
- Configure Group Policy
- Apply the principle of least privilege
- Delegate password-reset permissions to Helpdesk
- Automate Active Directory administration using PowerShell
- Provision multiple users from CSV data

---

# Infrastructure

## Azure Virtual Machines

Two Windows Server 2025 virtual machines were deployed.

### DC01 — Domain Controller

DC01 serves as the central identity and directory server for the environment.

**Configuration:**

- Windows Server 2025
- Active Directory Domain Services
- DNS Server
- Global Catalog
- Group Policy
- Static private IP: `10.0.0.4`
- Domain: `lab.local`

The domain controller was configured with a static private IP to provide a stable DNS endpoint for domain members.

### CLIENT01 — Domain-Joined Client

CLIENT01 was deployed in the same Azure Virtual Network as DC01.

**Configuration:**

- Windows Server 2025
- Same VNet as DC01
- DNS configured to use DC01
- Joined to `lab.local`
- Domain authentication tested through RDP

Although Windows Server is used for the client machine in this lab, it functions as a domain-joined client for authentication and Group Policy testing.

---

# Active Directory

## Domain

The Active Directory forest and domain were created as:

```text
lab.local
DC01 was promoted to the first domain controller in the environment.

Active Directory Domain Services and DNS were configured during the domain-controller deployment.

---

## Organizational Unit Structure

The OU structure was designed around branch location and policy boundaries rather than simply separating all users and computers into flat containers.

```text
lab.local
│
├── _Branches
│   │
│   └── Houston
│       │
│       ├── Users
│       ├── Workstations
│       └── Laptops
│
└── _Groups

This structure provides a foundation for applying targeted Group Policy and delegating administrative responsibilities.

