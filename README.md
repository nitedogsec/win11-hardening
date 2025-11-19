# 🛡️ Microsoft Defender Hardening Script

**All-in-one security hardening for Windows 10/11**

This PowerShell script provides a complete security hardening setup for **Microsoft Defender**.  
It enables enterprise-grade protections such as ASR rules, SmartScreen enforcement, ransomware protection, PowerShell logging, and more — without installing any third-party software.

Ideal for users who want **maximum protection with minimal performance impact**.

---

## ✨ Features

### ✔ Backup of Current Defender Configuration
Saves your existing settings before applying hardening.

### ✔ Core Microsoft Defender Protections
- Realtime protection  
- Cloud-based detection  
- Sample submission  
- PUA (Potentially Unwanted Application) protection  

### ✔ Attack Surface Reduction (ASR) Rules
Blocks:
- Office child processes  
- Malicious scripts  
- LSASS credential theft  
- Persistence mechanisms  
- USB malware  
- Executable content from email  

### ✔ PowerShell Hardening
- Requires signed scripts  
- Enables ScriptBlockLogging  
- Enables full PowerShell transcription  

### ✔ SmartScreen Enforcement
Blocks untrusted apps and requires admin approval.

### ✔ Anti-Ransomware Protection
Enables **Controlled Folder Access** for critical user paths.

### ✔ Office Macro Hardening
Blocks macros originating from the internet.

### ✔ Enhanced Defender Notifications
Ensures user is notified about critical security events.

---

## 🚀 Usage

### 1️⃣ Remove Any Third-Party Antivirus (Recommended)
If migrating from Norton, use the official cleanup tool:

> **[Norton Remove and Reinstall Tool (NRnR)](https://support.norton.com/sp/en/us/home/current/solutions/v60392881)**  

This ensures no leftover drivers or filters interfere with Defender.

---

### 2️⃣ Run the Script

Run PowerShell **as Administrator**:

```powershell
# Open PowerShell as admin
# Copy/paste the defender-hardening.ps1 script
# Press Enter
# Restart your computer when prompted
