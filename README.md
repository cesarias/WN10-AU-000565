# WN10-AU-000565
# Windows 10 STIG Remediation: WN10-AU-000565

## 🔐 STIG Overview

**STIG ID:** WN10-AU-000565 &#x20;
**Title:** Windows 10 must be configured to audit Other Logon/Logoff Events Failures. &#x20;
**Category:** Audit Policy &#x20;
**Severity:** Medium &#x20;
**Reference:** [DISA STIG](https://public.cyber.mil/stigs/)  \\

---

## 🎯 Objective

Remediate STIG finding `WN10-AU-000565` by enabling auditing of "Other Logon/Logoff Events - Failures". This includes manual and automated (PowerShell) remediation, validated by Tenable scans before and after changes.

---

## 🧪 Steps Performed

### 1. Initial Vulnerability Scan

* **Tool:** Tenable.sc or Nessus (STIG Plugin Enabled)
* **Platform:** Azure Windows 10 VM
* **Result:** Finding `WN10-AU-000565` flagged as **non-compliant**
<img width="1000" alt="image" src="https://i.imgur.com/iFYAiny.png">
### 2. Manual Remediation

* **Steps:**

  * Open `gpedit.msc`
  * Navigate to:
    `Computer Configuration > Windows Settings > Security Settings > Advanced Audit Policy Configuration > Audit Policies > Logon/Logoff`
  * Double-click **Other Logon/Logoff Events**
  * Set **Failure** to **Enabled**
 
<img width="1000" alt="image" src="https://i.imgur.com/8h0ofUA.jpeg">
<img width="1000" alt="image" src="https://i.imgur.com/fvcrHvj.png">
* **Verification:** Re-scan with Tenable shows compliance
<img width="1000" alt="image" src="https://i.imgur.com/SJrhIqT.png">


### 3. Undo Manual Fix (Optional)

* Revert the setting to **Not Configured**
* Re-scan to confirm STIG is once again **non-compliant**
<img width="1000" alt="image" src="https://i.imgur.com/GHZPleS.png">
<img width="1000" alt="image" src="https://i.imgur.com/GP34IaP.png">
### 4. PowerShell Remediation

```powershell
# Enable auditing of Other Logon/Logoff Events - Failure
auditpol /set /subcategory:"Other Logon/Logoff Events" /failure:enable
```

* **File:** `remediate-WN10-AU-000565.ps1`
* **Execution:** Run in elevated PowerShell window (Run as Administrator)
<img width="1000" alt="image" src="https://i.imgur.com/JkUSDMn.png">
* **Verification:** Final scan confirms STIG compliance
<img width="1000" alt="image" src="https://i.imgur.com/e90oSCa.png">
---

## 📂 Supporting Files

* `remediate-WN10-AU-000565.ps1` – PowerShell remediation script
* `scan-before.nessus` – Tenable scan before remediation
* `scan-after.nessus` – Tenable scan after remediation
* `images/` folder – Contains screenshots of each step

---

## 🔄 Before and After Comparison

| State      | Screenshot                                                             |
| ---------- | ---------------------------------------------------------------------- |
| Before Fix | <img width="1000" alt="image" src="https://i.imgur.com/iFYAiny.png">   |
| After Fix  | <img width="1000" alt="image" src="https://i.imgur.com/e90oSCa.png">   |

---

🧪 Simulating Detection: Triggering a Failure

To confirm that the audit policy works:

Attempt a failed RDP login from another machine or simulate a failed local login (wrong password).

Then run:

eventvwr.msc

Navigate to: Windows Logs > Security

Filter logs for Event ID 4625 (failed logon)

Screenshot of Log Entry: 

<img width="1000" alt="image" src="https://i.imgur.com/X0gdJcT.png">

## 📚 Lessons Learned

* Configuring logon/logoff failure audits is essential for identifying unauthorized access attempts.
* PowerShell provides a repeatable method for policy enforcement.
* Tenable validates security posture changes effectively in real time.

---

## 👤 Author

**Name:** Cesar Arias &#x20;
**Role:** Cybersecurity Student | Portfolio Project &#x20;
**Contact:** cesarias2022@gmail.com

---

## 🗓️ Date Completed

**Remediation Date:** 7/11/2025
---

## ✏️ Version

**Version:** 1.0 &#x20;
**Environment:** Azure Windows 10 VM &#x20;
**Tooling:** Tenable + PowerShell + Group Policy
