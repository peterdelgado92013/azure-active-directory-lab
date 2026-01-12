<p align="center">
  <img src="https://img.shields.io/badge/Active%20Directory-Domain%20Services-0078D4?style=for-the-badge&logo=windows&logoColor=white" />
</p>


# Active Directory Domain Services Lab (Azure)

**Enterprise-style Active Directory implementation hosted in Microsoft Azure.**  
This project demonstrates installing Active Directory Domain Services (AD DS), promoting a Windows Server to a Domain Controller, joining a Windows client to the domain, organizing users and computers with OUs, enabling Remote Desktop access for domain users, and automating bulk user creation with PowerShell.

---

## 🔥 Project Objectives
- Deploy Active Directory Domain Services (AD DS)
- Promote a Windows Server VM to a Domain Controller
- Create and manage Organizational Units (OUs)
- Configure Domain Admin and standard domain users
- Join a Windows client VM to the domain
- Enable Remote Desktop access for non-admin users
- Automate user provisioning using PowerShell
- Verify domain functionality using ADUC

---

## 🧰 Technologies Used
- Microsoft Azure (Virtual Machines, Virtual Network)
- Windows Server (Domain Controller)
- Windows 10/11 Client
- Active Directory Domain Services (AD DS)
- Active Directory Users & Computers (ADUC)
- PowerShell / PowerShell ISE
- Remote Desktop Protocol (RDP)

---

## 🖥️ Lab Environment
**Azure Virtual Machines**
- **DC-1** — Windows Server (Domain Controller)
- **Client-1** — Windows 10/11 (Domain-joined client)

> VMs can be safely stopped in the Azure Portal when not in use to avoid unnecessary charges.

---

## 🚀 Part 1 — Domain Controller Setup & Client Join

### 1️⃣ Install Active Directory Domain Services
- Installed AD DS on DC-1
- Promoted server to Domain Controller
- Created a new forest (`mydomain.com`)

📸 `screenshots/part1/adds-installation.png`

---

### 2️⃣ Create OUs and Domain Admin Account
- Created `_EMPLOYEES` and `_ADMINS` OUs
- Created Domain Admin user (`jane_admin`)
- Assigned Domain Admin privileges

📸 `screenshots/part1/ous-and-admin.png`

---

### 3️⃣ Join Client VM to Domain
- Configured Client-1 DNS to point to DC-1
- Joined Client-1 to domain
- Verified domain join in ADUC
- Organized Client-1 under `_CLIENTS` OU

📸 `screenshots/part1/client-domain-join.png`

---

## 🔐 Part 2 — RDP Access & User Automation

### 4️⃣ Enable Remote Desktop for Domain Users
- Allowed **Domain Users** Remote Desktop access on Client-1
- Verified non-admin domain login via RDP

📸 `screenshots/part2/rdp-domain-users.png`

> In production environments, this would typically be handled using Group Policy.

---

### 5️⃣ Bulk User Creation with PowerShell
- Created multiple domain users via PowerShell script
- Users automatically placed in `_EMPLOYEES` OU
- Verified accounts in Active Directory Users & Computers

📸 `screenshots/part2/powershell-user-creation.png`

📂 Script location:


