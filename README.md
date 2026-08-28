# Active Directory Administration & Security Lab

## Executive Summary
This repository documents advanced Active Directory administration and security configuration simulating enterprise IT support tickets. Each scenario was completed using both **Manual GUI Administration** and **Automated PowerShell Scripting**, with ticket tracking in Jira Service Management.

* **Full Step-by-Step Walkthrough:** [Download Complete PDF Documentation](./Project%202_%20Active%20Directory%20Administration%20%26%20Security.pdf)

---

## Technical Stack & Environment
* **Directory Services:** Active Directory Domain Services (AD DS) on Windows Server 2022
* **Cloud Infrastructure:** AWS EC2
* **Scripting & Automation:** PowerShell
* **ITSM / Ticketing:** Jira Service Management

---

## Simulated Ticket Matrix

| Ticket ID | Issue / Request | Primary Method (GUI) | Automation Method (PowerShell) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **ADSEC-001** | Create Organizational Unit Structure | ADUC Console | `New-ADOrganizationalUnit` | Resolved |
| **ADSEC-002** | Create & Configure Security Groups | ADUC Console | `New-ADGroup` | Resolved |
| **ADSEC-003** | Configure Fine-Grained Password Policy | AD Administrative Center | `New-ADFineGrainedPasswordPolicy` | Resolved |
| **ADSEC-004** | Delegate Administrative OU Permissions | ADUC Delegation Wizard | `Set-Acl` / PowerShell | Resolved |
| **ADSEC-005** | Audit & Review Inactive User Accounts | ADUC Search | `Search-ADAccount` | Resolved |

---

## Ticket Execution Workflow Example

### Featured Ticket ADSEC-001: Create Organizational Unit Structure

#### Method 1: Manual GUI Execution
1. **Scenario & Intake:** Reviewed ticket request in Jira Service Management queue to create a new Organizational Unit for the IT department.
2. **Step-by-Step Implementation:** Opened Server Manager on the Domain Controller, launched **Active Directory Users and Computers** (`dsa.msc`), right-clicked domain root `mydclab.local`, selected **New > Organizational Unit**, entered `IT-OU` into the **Name** field with accidental deletion protection checked, and clicked **OK**.
3. **Verification:** Verified `IT-OU` creation and placement directly under `mydclab.local` in the ADUC directory tree.

#### Method 2: PowerShell Automation
1. **Script Development:** Executed `New-ADOrganizationalUnit -Name "IT-OU" -Path "DC=mydclab,DC=local"` and enforced deletion protection using `Set-ADOrganizationalUnit -Identity "OU=IT-OU,DC=mydclab,DC=local" -ProtectedFromAccidentalDeletion $true` in an elevated PowerShell session.
2. **Execution & Audit:** Verified OU creation and attributes programmatically using `Get-ADOrganizationalUnit -Filter "Name -eq 'IT-OU'"`.

#### Resolution Summaries

**Ticket Resolution Summary (GUI Method)**
* **Issue Description:** Create a dedicated Organizational Unit for the IT department to organize users and administrative policies.
* **Actions Taken (GUI):** Opened ADUC (`dsa.msc`), created `IT-OU` under domain root `mydclab.local` with accidental deletion protection enabled, and verified visual placement.
* **Resolution:** OU created and verified via GUI. Ticket closed in Jira.

**Ticket Resolution Summary (PowerShell Method)**
* **Issue Description:** Automated creation of the IT department Organizational Unit.
* **Actions Taken (PowerShell):** Executed `New-ADOrganizationalUnit` and `Set-ADOrganizationalUnit` to provision `IT-OU` under `DC=mydclab,DC=local` with accidental deletion protection, then audited via `Get-ADOrganizationalUnit`.
* **Resolution:** OU created programmatically and audited via command line. Ticket closed in Jira.
