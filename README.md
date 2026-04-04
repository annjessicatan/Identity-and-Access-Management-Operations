# 🏛️ Active Directory Basics — TryHackMe Walkthrough

> **Portfolio Project:** Complete walkthrough of TryHackMe's "Active Directory Basics" room  
> **Role Simulated:** Junior Domain Administrator for THM.local  
> **Date Completed:** 04/02/2026  
> **Tools Used:** Active Directory Users & Computers (ADUC), Group Policy Management Console (GPMC), PowerShell, RDP, Windows Server

## 📌 Overview

Microsoft Active Directory (AD) is the backbone of identity and access management in over 90% of Fortune 1000 companies. This repository documents my hands-on journey learning AD fundamentals by acting as a newly hired IT administrator tasked with organizing, securing and managing the **THM.local** domain.

Through this lab, I moved beyond theory and actually:
- Created/deleted Organizational Units (OUs)
- Delegated administrative privileges
- Managed computer objects
- Implemented real Group Policy Objects (GPOs)
- Retrieved a flag proving successful configuration

## 🎯 Skills Demonstrated

| Category | Specific Skills |
|----------|----------------|
| **AD Management** | Navigating ADUC, creating OUs, deleting protected OUs, understanding default containers |
| **Delegation** | Granting password reset privileges to IT support staff without Domain Admin rights |
| **Computer Management** | Organizing workstations/servers into logical OUs, understanding computer account naming (`DC01$`) |
| **Group Policy** | Creating GPOs, linking to OUs, configuring password policies, restricting Control Panel access, forcing screen locks |
| **PowerShell** | `Set-ADAccountPassword`, `Set-ADUser`, `gpupdate /force` |
| **Authentication** | Understanding Kerberos (TGT, TGS) vs NetNTLM challenge-response |


## 🖼️ Screenshot Evidence by Task

<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr>
      <th style="width: 10%; text-align: left; padding: 12px;">Task</th>
      <th style="width: 50%; text-align: left; padding: 12px;">Screenshot</th>
      <th style="width: 40%; text-align: left; padding: 12px;">What It Demonstrates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 3</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/aa1e1605-ff48-4cc6-8c91-9f8542f1c2f7" width="100%" alt="THM OU hierarchy"></td>
      <td style="padding: 12px; vertical-align: top;">THM OU with 5 child OUs (IT, Management, Marketing, R&D, Sales)</td>
    </tr> 
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 3</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/d7ac7b7d-34f4-4661-9df2-1e98172001fbf" width="100%" alt="Created Custom Student OU"></td>
      <td style="padding: 12px; vertical-align: top;">Created custom "Students" OU</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 3</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/1aa91d80-18fe-4c82-afe7-02d12b95c155" width="100%" alt="Disabled users"></td>
      <td style="padding: 12px; vertical-align: top;">Disabled users whose names aren't showing in the existing AD OUs</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 4</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/0cf967e7-797e-4a49-ac45-634c87f18931" width="100%" alt="deletion protection"></td>
      <td style="padding: 12px; vertical-align: top;">Encountered accidental deletion protection (problem-solving moment)</td>
    </tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 4</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/f8323401-cac3-49e2-b19d-24820ccdb218" width="100%" alt="enabled advanced features"></td>
      <td style="padding: 12px; vertical-align: top;">Enabled Advanced Features in View menu</td>
    </tr>
    <tr> 
      <td style="padding: 12px; vertical-align: top;"><strong>Task 4</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/29168a63-4719-440b-84a0-5cbe15efdd3f" width="100%" alt="Unchecked protection"></td>
      <td style="padding: 12px; vertical-align: top;">Unchecked "Protect from accidental deletion"</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 4</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/6827d0c4-07be-43d7-9a61-e0791b7ac4b7" width="100%" alt="delegation of password"></td>
      <td style="padding: 12px; vertical-align: top;">Delegated password reset to Phillip (wizard steps grouped)</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 4</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/e2a0178f-88cc-4cbc-acee-b6a490fbcd84" width="100%" alt="set ADAccount and password"></td>
      <td style="padding: 12px; vertical-align: top;"><code>Set-ADAccountPassword</code> and <code>Set-ADUser</code> commands</td>
    </tr>
    <tr> 
      <td style="padding: 12px; vertical-align: top;"><strong>Task 4</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/b098f8d1-3a8d-4f0e-a68a-a92ada45eaa0" width="100%" alt="set ADAccount and password"></td>
      <td style="padding: 12px; vertical-align: top;"><strong>Flag retrieved</strong> from Sophie's desktop ✅</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 5</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/c77eaf1b-f5eb-4b33-b1fc-9ec03c2409f2" width="100%" alt="set ADAccount and password"></td>
      <td style="padding: 12px; vertical-align: top;">All machines in default "Computers" container</td>
    </tr>
    <tr> 
      <td style="padding: 12px; vertical-align: top;"><strong>Task 5</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/74d5e88d-bfc6-48d9-997c-102f1636e9da" width="100%" alt="set ADAccount and password"></td>
      <td style="padding: 12px; vertical-align: top;">Workstations + Servers OUs created under thm.local</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 5</strong></td>
      <td style="padding: 12px; vertical-align: top;"><img src="https://github.com/user-attachments/assets/80920ca7-39c0-45e3-8204-68af6946d2ef" width="100%" alt="set ADAccount and password"></td>
      <td style="padding: 12px; vertical-align: top;">PCs/laptops moved to Workstations, servers to Servers OU</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 6</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>task-6/gpmc-overview.png</code></td>
      <td style="padding: 12px; vertical-align: top;">Group Policy Management Console with full OU hierarchy</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 6</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>task-6/default-password-policy.png</code></td>
      <td style="padding: 12px; vertical-align: top;">Changed minimum password length to 10 characters</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 6</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>task-6/restrict-control-panel.png</code></td>
      <td style="padding: 12px; vertical-align: top;">Enabled "Prohibit Access to Control Panel" policy</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 6</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>task-6/gpo-linking.png</code></td>
      <td style="padding: 12px; vertical-align: top;">Restrict Control Panel linked to Marketing, Management, Sales OUs</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 6</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>task-6/auto-lock-policy.png</code></td>
      <td style="padding: 12px; vertical-align: top;">Set inactivity limit to 5 minutes</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Task 6</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>task-6/verification-mark-denied.png</code></td>
      <td style="padding: 12px; vertical-align: top;"><strong>Logged in as Mark</strong> — Control Panel access denied ✅</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Diagrams</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>diagrams/kerberos-flow.png</code></td>
      <td style="padding: 12px; vertical-align: top;">Visual: Client → KDC → TGT → TGS → Service</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Diagrams</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>diagrams/netntlm-flow.png</code></td>
      <td style="padding: 12px; vertical-align: top;">Visual: Challenge-response mechanism</td>
    </tr>
    <tr>
      <td style="padding: 12px; vertical-align: top;"><strong>Diagrams</strong></td>
      <td style="padding: 12px; vertical-align: top;"><code>diagrams/trees-forests.png</code></td>
      <td style="padding: 12px; vertical-align: top;">thm.local → uk.thm.local + us.thm.local + MHT Inc. forest</td>
    </tr>
  </tbody>
</table>

## 🔑 Key Concepts I Learned

### 1. OUs vs Security Groups (Critical Distinction)
| | **Organizational Units (OUs)** | **Security Groups** |
|--|-------------------------------|---------------------|
| **Purpose** | Apply policies (GPOs) | Grant permissions to resources |
| **Membership** | One OU per user/computer | Many groups per user |
| **Example** | Sales OU gets different desktop background | "Sales Share" group can access \\fileserver\sales |

### 2. Group Policy Objects (GPOs) Inheritance
- GPOs apply to the linked OU **and all child OUs** (unless blocked)
- Computer Configurations apply to computers; User Configurations apply to users
- Changes sync via SYSVOL share — force with `gpupdate /force`

### 3. Delegation Without Domain Admin Rights
- Granted Phillip (IT Support) ability to reset passwords for Sales, Marketing, Management OUs
- Verified by logging as Phillip and using PowerShell — no ADUC access needed

### 4. Authentication Protocols
| Protocol | Default? | How It Works |
|----------|----------|--------------|
| **Kerberos** | Yes (modern Windows) | Ticket-based: TGT → TGS → Service access |
| **NetNTLM** | Legacy | Challenge-response, no password transmitted |

### 5. Trees, Forests & Trusts
- **Tree:** Multiple domains sharing same namespace (thm.local → uk.thm.local)
- **Forest:** Multiple trees with different namespaces (THM + MHT Inc.)
- **Trust:** Two-way by default in trees/forests; allows cross-domain authorization

## ✅ Lab Completion Verification

All objectives were successfully completed:

- [x] Deleted R&D OU (disabled accidental deletion protection first)
- [x] Matched AD users to organizational chart (added/deleted as needed)
- [x] Delegated password reset control to Phillip (IT Support)
- [x] Retrieved flag from `THM\sophie` desktop after resetting her password
- [x] Created Workstations and Servers OUs
- [x] Moved computer objects from default "Computers" container
- [x] Created "Restrict Control Panel Access" GPO → linked to non-IT OUs
- [x] Created "Auto Lock Screen" GPO (5 minutes) → linked to root domain
- [x] Verified Control Panel restriction as `THM\Mark`
- [x] Understood Kerberos vs NetNTLM (diagrams created)
- [x] Learned Trees, Forests, and Trust relationships

## 🖥️ Lab Environment

| Detail | Information |
|--------|-------------|
| Platform | TryHackMe |
| Room | Active Directory Basics |
| Domain | THM.local |
| Domain Controller | Windows Server (DC) |
| AttackBox | Used for RDP connections |
| Credentials Used | Administrator, Phillip, Mark, Sophie |

## 📝 Commands Reference

```powershell
# Force GPO sync on any machine
gpupdate /force

# Reset user password (requires delegation or admin rights)
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString)

# Force password change at next logon
Set-ADUser -ChangePasswordAtLogon $true -Identity sophie
```

## 🚀 What's Next?

This room is foundational. My learning roadmap continues with:

| Next Step | Platform | Focus |
|-----------|----------|-------|
| Active Directory Hardening | TryHackMe | Securing AD configurations |
| Compromising Active Directory | TryHackMe | Common AD attack vectors (Kerberoasting, AS-REP Roasting, Golden Ticket) |
| AD Pentesting | HackTheBox / Lab | Hands-on red team exercises |

---

## 📫 Connect With Me

- **LinkedIn:** www.linkedin.com/in/annjessicatan
- **GitHub:** [[Your GitHub Profile]](https://github.com/annjessicatan)
- **Portfolio:** N/A
- **Email:** ajessicavtan@gmail.com

---

## 📄 License

This repository is for educational purposes. All screenshots were taken during legitimate TryHackMe lab time. No proprietary or confidential information is included.

---

⭐ *If you found this walkthrough helpful, consider starring the repository!*
