# Active Directory Domain Services Lab (Azure) — DC + Client Join + Bulk User Creation

This project demonstrates installing **Active Directory Domain Services (AD DS)** on a Windows Server VM in Azure, promoting it to a **Domain Controller**, joining a Windows Client VM to the domain, configuring Remote Desktop access for domain users, and creating multiple domain users using PowerShell.

---

## 🔥 Lab Goals
- Install and configure **Active Directory Domain Services**
- Promote server to **Domain Controller** and create a new forest (`mydomain.com`)
- Create OUs and a **Domain Admin** account
- Join a client VM to the domain
- Configure **Remote Desktop access** for non-admin domain users
- Bulk create domain users via **PowerShell**
- Verify objects in **Active Directory Users & Computers (ADUC)**

---

## 🧰 Technologies Used
- Microsoft Azure (VMs / Virtual Network)
- Windows Server (Domain Controller)
- Windows 10/11 Client VM
- Active Directory Domain Services (AD DS)
- Active Directory Users & Computers (ADUC)
- PowerShell / PowerShell ISE
- Remote Desktop Protocol (RDP)

---

## 🖥️ Environment
### Azure Virtual Machines
- **DC-1** (Windows Server) — Domain Controller
- **Client-1** (Windows 10/11) — Domain-joined workstation

> If you're done working for the day, stop the VMs in Azure to save money.

---

# ✅ Part 1 — Install AD DS + Promote DC + Join Client

## 1) Turn on VMs (Azure Portal)
- [ ] Start **DC-1**
- [ ] Start **Client-1**

📸 Screenshot: `screenshots/part1/01-vms-running.png`

---

## 2) Install Active Directory Domain Services (DC-1)
1. RDP into **DC-1**
2. Server Manager → Add roles and features
3. Select **Active Directory Domain Services**
4. Install

📸 Screenshot: `screenshots/part1/02-adds-installed.png`

---

## 3) Promote DC-1 to Domain Controller
1. Click the flag notification → **Promote this server to a domain controller**
2. Select: **Add a new forest**
3. Domain name: `mydomain.com` *(or your custom domain — just stay consistent)*
4. Complete the wizard and restart

✅ After reboot, log in as:
- `mydomain.com\labuser`

📸 Screenshot: `screenshots/part1/03-new-forest.png`

---

## 4) Create OUs + Domain Admin User (ADUC)
Open **Active Directory Users and Computers (ADUC)**

### Create Organizational Units
- [ ] Create OU: `_EMPLOYEES`
- [ ] Create OU: `_ADMINS`

📸 Screenshot: `screenshots/part1/04-ous-created.png`

### Create Domain Admin User
Create a user:
- Name: **Jane Doe**
- Username: `jane_admin`
- Password: `Cyberlab123!`

Then:
- [ ] Add `jane_admin` to **Domain Admins** group

📸 Screenshot: `screenshots/part1/05-jane-admin-domain-admins.png`

✅ Log out of DC-1 and log back in as:
- `mydomain.com\jane_admin`

> Use `jane_admin` as the admin account going forward.

---

## 5) Join Client-1 to the Domain
### Confirm DNS Points to DC-1 Private IP (Azure)
- [ ] Client-1 DNS is set to DC-1 Private IP (already done)
- [ ] Restart Client-1 (already done)

📸 Screenshot: `screenshots/part1/06-client-dns.png`

### Join Domain from Client-1
1. RDP into **Client-1** as local admin:
   - `labuser`
2. System → About → Rename this PC (advanced) → Domain
3. Join: `mydomain.com`
4. Restart

📸 Screenshot: `screenshots/part1/07-client-joined-domain.png`

---

## 6) Verify Client-1 appears in ADUC (DC-1)
1. Open ADUC on DC-1
2. Confirm `Client-1` is present
3. Create OU `_CLIENTS`
4. Drag `Client-1` into `_CLIENTS`

📸 Screenshot: `screenshots/part1/08-client-moved-ou.png`

---

# ✅ Part 2 — RDP Access for Domain Users + Bulk Create Users

## 1) Turn on VMs (Azure Portal)
- [ ] Start **DC-1**
- [ ] Start **Client-1**

📸 Screenshot: `screenshots/part2/01-vms-running.png`

---

## 2) Allow Domain Users Remote Desktop on Client-1
1. Log into Client-1 as:
   - `mydomain.com\jane_admin`
2. Open: **System Properties**
3. Remote tab → Remote Desktop
4. Allow Remote Desktop
5. Add **Domain Users** to allowed users

📸 Screenshot: `screenshots/part2/02-rdp-domain-users.png`

✅ Now any domain user can RDP into Client-1  
*(In real environments, this is typically managed with Group Policy.)*

---

## 3) Bulk Create Users with PowerShell (DC-1)
1. Log into DC-1 as:
   - `mydomain.com\jane_admin`
2. Open **PowerShell ISE** as Administrator
3. Create a script:
   - `scripts/create-users.ps1`
4. Run it and observe accounts being created

📸 Screenshot: `screenshots/part2/03-powershell-users-created.png`

### Verify users in ADUC
- [ ] Open ADUC
- [ ] Confirm users appear inside `_EMPLOYEES`

📸 Screenshot: `screenshots/part2/04-aduc-employees-populated.png`

---

## 4) Test Login (Client-1)
- [ ] Try logging into Client-1 as one of the created users  
  *(Use the password inside the script)*

📸 Screenshot: `screenshots/part2/05-login-test.png`

---

## ✅ Results / What This Demonstrates
- Domain Controller creation and AD DS deployment
- Domain join + OU organization
- Admin account management + permissions
- Remote Desktop access configuration for standard users
- PowerShell automation for user provisioning

---

## 🧹 Cost Management
If you are done for the day:
- Stop the VMs in Azure Portal to avoid charges

---

## 📌 Next Steps (Future Labs)
- Group Policy (GPO) to manage RDP permissions at scale
- Password policies + account lockout rules
- File shares + NTFS permissions
- DNS troubleshooting + domain services monitoring
