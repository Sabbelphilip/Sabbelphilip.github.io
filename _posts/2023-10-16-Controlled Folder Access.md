---
title: Defender for Endpoint - Controlled Folder Access
date: 2023-10-16 12:00:00 +0000
categories: [Microsoft Defender for Endpoint]
tags: [microsoft defender, security, microsoft defender for endpoint, controlled folder access, attack surface reduction]     # TAG names should always be lowercase
---



# Defender for Endpoint - Controlled Folder Access

## Docs and Sources

| Description                     |     Link                                                                                                                                                                              |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MSLearn Controlled Folder Access | [MSLearn - Controlled Folder Access](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/controlled-folders?view=o365-worldwide)               |
|                                 |                                                                                                                                                                                   |

## Requirements

- Defender for Endpoint P1 / P2
- Windows 10, version 1709 and later
- Windows 11
- Windows 2012 R2, 2016, 2019, 2022

## Description

The Controlled Folder Access feature in Microsoft Defender for Endpoint is designed to safeguard critical files and folders on Windows devices against unwanted alterations by malicious activities or ransomware. It monitors and restricts access to selected directories to maintain the integrity of sensitive data. Its recommended to use this feature in Audit Mode first to analyse the impact on the environment!


## Configuration

**Configuration by Intune Policy**

1. Intune → Endpoint Security → Attack Surface Reduction → Create Policy
2. Select Windows 10, Windows 11, and Windows Server
3. Select Attack Surface Reduction Rules

![Controlled Folder Access Configuration](/img/posts/20231016/CFAconfig.png)


## Troubleshooting

### Check CFA Status:

- 0 - Disabled
- 1 - Enabled
- 2 - Audit Mode

```
Get-MpPreference | select EnableControlledFolderAccess
```

### Change CFA Status:

- Enabled
- AuditMode
- Disabled

```
Set-MpPreference -EnableControlledFolderAccess Enabled
```

### Check CFA Alerts:

Defender Advanced Hunting Query:

```DeviceEvents
| where ActionType in ('ControlledFolderAccessViolationAudited','ControlledFolderAccessViolationBlocked')
```

### Add Application to Allow List (Nur bei Notfällen)
```
Add-MpPreference -ControlledFolderAccessAllowedApplications "<Application Path>"
```

### Add Folder to Protected Folder List (Nur bei Notfällen)
```
Add-MpPreference -ControlledFolderAccessProtectedFolders "<Folder Path>"
```