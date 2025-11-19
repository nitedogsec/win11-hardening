# ============================================
# HARDENING MICROSOFT DEFENDER - All in one
# By n1t3d0g
# ============================================

Write-Host "Iniciando hardening de Microsoft Defender..." -ForegroundColor Cyan

# --------------------------------------------
# 1. BACKUP CURRENT CONFIGURATION
# --------------------------------------------
Write-Host "[1/9] Backing up current Defender configuration..." -ForegroundColor Yellow
$backupPath = "$env:USERPROFILE\Desktop\DefenderBackup_$(Get-Date -Format 'yyyyMMdd_HHmmss').txt"
Get-MpPreference | Out-File $backupPath
Write-Host "Backup guardado en: $backupPath" -ForegroundColor Green


# --------------------------------------------
# 2. ENABLE CORE DEFENDER FEATURES
# --------------------------------------------
Write-Host "[2/9] Enabling core Defender features..." -ForegroundColor Yellow

Set-MpPreference -DisableRealtimeMonitoring $false
Set-MpPreference -MAPSReporting Advanced
Set-MpPreference -SubmitSamplesConsent Always
Set-MpPreference -DisableArchiveScanning $false
Set-MpPreference -DisableIntrusionPreventionSystem $false
Set-MpPreference -DisableIOAVProtection $false
Set-MpPreference -PUAProtection Enabled

Write-Host "Realtime, Cloud, PUA and core protections enabled." -ForegroundColor Green


# --------------------------------------------
# 3. ENABLE ASR RULES (ATTACK SURFACE REDUCTION)
# --------------------------------------------
Write-Host "[3/9] Enabling recommended ASR rules..." -ForegroundColor Yellow

$ASRRules = @(
"BE9BA2D9-53EA-4CDC-84E5-9B1EEEE46550",  # Block executable content from email
"D4F940AB-401B-4EFC-AADC-AD5F3C50688A",  # Block Office from creating child processes
"3B576869-A4EC-4529-8536-B80A7769E899",  # Block Office from creating executable content
"75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84",  # Block Office apps from injecting code
"26190899-1602-49e8-8b27-eb1d0a1ce869",  # Block credential stealing from LSASS
"5BEB7EFE-FD9A-4556-801D-275E5FFC04CC",  # Block execution from USB devices
"D1E49AAC-8F56-4280-B9BA-993A6D77406C",  # Block obfuscated or malicious scripts
"9E6D062C-4F38-4DF0-8A4B-3B8E1E3C9C39"   # Block persistence mechanisms
)

foreach ($rule in $ASRRules) {
    Add-MpPreference -AttackSurfaceReductionRules_Ids $rule -AttackSurfaceReductionRules_Actions Enabled
}

Write-Host "ASR rules enabled." -ForegroundColor Green


# --------------------------------------------
# 4. HARDEN POWERSHELL
# --------------------------------------------
Write-Host "[4/9] Hardening PowerShell..." -ForegroundColor Yellow

# Require signed scripts
Set-ExecutionPolicy AllSigned -Scope LocalMachine -Force

# Enable ScriptBlock and transcription logging
New-Item -Path HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging -Force | Out-Null
Set-ItemProperty HKLM:\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging -Name EnableScriptBlockLogging -Value 1

New-Item -Path HKLM:\Software\Policies\Microsoft\Windows\PowerShell\Transcription -Force | Out-Null
Set-ItemProperty HKLM:\Software\Policies\Microsoft\Windows\PowerShell\Transcription -Name EnableTranscripting -Value 1

Write-Host "PowerShell hardened." -ForegroundColor Green


# --------------------------------------------
# 5. ENABLE SMARTSCREEN
# --------------------------------------------
Write-Host "[5/9] Enabling SmartScreen..." -ForegroundColor Yellow

New-Item -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Explorer" -Force | Out-Null
Set-ItemProperty "HKLM:\Software\Microsoft\Windows\CurrentVersion\Explorer" SmartScreenEnabled "RequireAdmin"

Write-Host "SmartScreen enabled." -ForegroundColor Green


# --------------------------------------------
# 6. ENABLE ANTI-RANSOMWARE (CONTROLLED FOLDER ACCESS)
# --------------------------------------------
Write-Host "[6/9] Enabling Controlled Folder Access (anti-ransomware)..." -ForegroundColor Yellow

Set-MpPreference -EnableControlledFolderAccess Enabled

Write-Host "Controlled Folder Access enabled." -ForegroundColor Green


# --------------------------------------------
# 7. BLOCK UNSAFE OFFICE MACROS
# --------------------------------------------
Write-Host "[7/9] Blocking unsafe Office macros..." -ForegroundColor Yellow

New-Item -Path "HKCU:\Software\Microsoft\Office\Common\Security" -Force | Out-Null
Set-ItemProperty "HKCU:\Software\Microsoft\Office\Common\Security" "BlockContentExecutionFromInternet" 1

Write-Host "Macro blocking enabled." -ForegroundColor Green


# --------------------------------------------
# 8. ENABLE IMPORTANT NOTIFICATIONS
# --------------------------------------------
Write-Host "[8/9] Enabling enhanced notifications..." -ForegroundColor Yellow

Set-MpPreference -DisableEnhancedNotifications $false

Write-Host "Notifications enabled." -ForegroundColor Green


# --------------------------------------------
# 9. FINISH
# --------------------------------------------
Write-Host "[9/9] Hardening completed successfully!" -ForegroundColor Cyan
Write-Host "Please restart your computer to apply all changes." -ForegroundColor Cyan
