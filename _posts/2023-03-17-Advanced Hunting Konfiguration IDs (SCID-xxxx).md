---
title: Advanced Hunting Konfiguration IDs (SCID-xxxx)
date: 2023-03-17 12:00:00 +0000
categories: [Microsoft Defender]
tags: [microsoft defender, security, advanced hunting]     # TAG names should always be lowercase
---
# Advanced Hunting Konfiguration IDs


## Docs and Sources

| Description                                   | Link                                                                                                                                                                                                   |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| MSDocs DeviceTvmSecureConfigurationAssessment | [MSDocs - DeviceTvmSecureConfigurationAssessment](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-devicetvmsecureconfigurationassessment-table?view=o365-worldwide) |


---

## Description

In Advanced Hunting is a table which contains a lot of Information about Konfiguration Settings. This Konfiguration Settings are bound to a unique KonfigurationID, formatted as "SCID-xxxx". THis allows us to query for this SCIDs and create Reports

### Example Query

```Kusto
DeviceTvmSecureConfigurationAssessment
| where ConfigurationId == "scid-2010"
| extend Result = case(IsApplicable == 0, "N/A", IsCompliant == 1, "GOOD", "BAD")
``` 

## Konfiguration IDs


### Smart Screen:
scid-2060   Set Microsoft Defender SmartScreen app and file checking to block or warn
scid-2061   Set Microsoft Defender SmartScreen Microsoft Edge site and download checking to block or warn

### Bitlocker: 
scid-2090	Encrypt all BitLocker-supported drives
scid-2091	Resume BitLocker protection on all drives
scid-2093	Ensure BitLocker drive compatibility


### Device Onboarding: 
scid-20000	Onboard devices to Microsoft Defender for Endpoint

### Firewall:
scid-2070	Turn on Microsoft Defender Firewall
scid-2071	Secure Microsoft Defender Firewall domain profile
scid-2072	Secure Microsoft Defender firewall private profile
scid-2073	Secure Microsoft Defender Firewall public profile

### Defender Antivirus:
scid-2003	Turn on Tamper Protection
scid-2010	Turn on Microsoft Defender Antivirus
Scid-2011	Signature Updates
scid-2012	Turn on real-time protection
scid-2013	Turn on PUA protection in block mode
scid-2016	Enable cloud-delivered protection
scid-90	    Enable Microsoft Defender Antivirus email scanning
scid-91	    Enable Microsoft Defender Antivirus real-time behavior monitoring
scid-92	    Enable Microsoft Defender Antivirus scanning of downloaded files and attachments
	
### Defender for Endpoint:
scid-2000	Turn on Microsoft Defender for Endpoint sensor
scid-2001	Fix Microsoft Defender for Endpoint sensor data collection
scid-2002	Fix Microsoft Defender for Endpoint impaired communications
scid-2004	Enable EDR in block mode
scid-2030	Update Microsoft Defender for Endpoint core components

### Credential Guard:
scid-2080	Turn on Microsoft Defender Credential Guard

### Exploit Guard:
scid-2020	Turn on all system-level Exploit protection settings
scid-2021	Set controlled folder access to enabled or audit mode

### Attack Surface Reduction:
scid-2500	Block executable content from email client and webmail
scid-2501	Block all Office applications from creating child processes
scid-2502	Block Office applications from creating executable content
scid-2503	Block Office applications from injecting code into other processes
scid-2504	Block JavaScript or VBScript from launching downloaded executable content
scid-2505	Block execution of potentially obfuscated scripts
scid-2506	Block Win32 API calls from Office macros
scid-2507	Block executable files from running unless they meet a prevalence, age, or trusted list criterion
scid-2508	Use advanced protection against ransomware
scid-2509	Block credential stealing from the Windows local security authority subsystem (lsass.exe)
scid-2510	Block process creations originating from PSExec and WMI commands
scid-2511	Block untrusted and unsigned processes that run from USB
scid-2512	Block Office communication application from creating child processes
scid-2513	Block Adobe Reader from creating child processes
scid-2514	Block persistence through WMI event subscription
scid-2515	Block abuse of exploited vulnerable signed drivers