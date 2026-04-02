# 🏛️ Active Directory Basics — TryHackMe Walkthrough

> **Portfolio Project:** Complete walkthrough of TryHackMe's "Active Directory Basics" room  
> **Role Simulated:** Junior Domain Administrator for THM.local  
> **Date Completed:** [Insert Date]  
> **Tools Used:** Active Directory Users & Computers (ADUC), Group Policy Management Console (GPMC), PowerShell, RDP, Windows Server

## 📌 Overview

Microsoft Active Directory (AD) is the backbone of identity and access management in over 90% of Fortune 1000 companies. This repository documents my hands-on journey learning AD fundamentals by acting as a newly hired IT administrator tasked with organizing, securing, and managing the **THM.local** domain.

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

## 📂 Repository Structure

- `README.md` — You are here
- `walkthrough.md` — Step-by-step lab guide with commands
- `glossary.md` — Key AD terms (OUs, GPOs, SPN, TGT, etc.)
- `assets/`
  - `screenshots/`
    - `task-3/` — ADUC interface, OU hierarchy
    - `task-4/` — Delegation, PowerShell, flag retrieval
    - `task-5/` — Computer OUs before/after
    - `task-6/` — GPO configurations, verification
    - `diagrams/` — Kerberos flow, Trust relationships
- `CHALLENGES.md` — Problems encountered & solutions


## 🖼️ Screenshot Evidence by Task

All screenshots are located in `/assets/screenshots/`. Below is a map of what each image proves:

| Task | Screenshot | What It Demonstrates |
|------|-----------|---------------------|
| **Task 3** | `task-3/ou-hierarchy.png` | THM OU with 5 child OUs (IT, Management, Marketing, R&D, Sales) |
| | `task-3/creating-students-ou.png` | Created custom "Students" OU (follow-along activity) |
| **Task 4** | `task-4/delete-protection-error.png` | Encountered accidental deletion protection (problem-solving moment) |
| | `task-4/advanced-features-enabled.png` | Enabled Advanced Features in View menu |
| | `task-4/disable-protection-checkbox.png` | Unchecked "Protect from accidental deletion" |
| | `task-4/delegation-wizard-collage.png` | Delegated password reset to Phillip (wizard steps grouped) |
| | `task-4/powershell-reset.png` | `Set-ADAccountPassword` and `Set-ADUser` commands |
| | `task-4/sophie-flag.png` | **Flag retrieved** from Sophie's desktop ✅ |
| **Task 5** | `task-5/computers-before.png` | All machines in default "Computers" container |
| | `task-5/ou-structure-final.png` | Workstations + Servers OUs created under thm.local |
| | `task-5/computers-after.png` | PCs/laptops moved to Workstations, servers to Servers OU |
| **Task 6** | `task-6/gpmc-overview.png` | Group Policy Management Console with full OU hierarchy |
| | `task-6/default-password-policy.png` | Changed minimum password length to 10 characters |
| | `task-6/restrict-control-panel.png` | Enabled "Prohibit Access to Control Panel" policy |
| | `task-6/gpo-linking.png` | Restrict Control Panel linked to Marketing, Management, Sales OUs |
| | `task-6/auto-lock-policy.png` | Set inactivity limit to 5 minutes |
| | `task-6/verification-mark-denied.png` | **Logged in as Mark** — Control Panel access denied ✅ |
| **Diagrams** | `diagrams/kerberos-flow.png` | Visual: Client → KDC → TGT → TGS → Service |
| | `diagrams/netntlm-flow.png` | Visual: Challenge-response mechanism |
| | `diagrams/trees-forests.png` | thm.local → uk.thm.local + us.thm.local + MHT Inc. forest |

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

- **LinkedIn:** [Your LinkedIn URL]
- **GitHub:** [Your GitHub Profile]
- **Portfolio:** [Your Website if applicable]
- **Email:** [Your Email]

---

## 📄 License

This repository is for educational purposes. All screenshots were taken during legitimate TryHackMe lab time. No proprietary or confidential information is included.

---

⭐ *If you found this walkthrough helpful, consider starring the repository!*
