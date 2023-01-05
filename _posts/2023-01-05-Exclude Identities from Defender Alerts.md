---
title: Exclude Identities from Microsoft Defender Identity Alerts
date: 2023-01-05 12:00:00 +0000
categories: [Microsoft Defender]
tags: [microsoft defender, security]     # TAG names should always be lowercase
---
# Exclude Entities from Microsoft Defender Identity Alerts


## Docs and Sources

| Description                                   | Link                                                                                 |
| --------------------------------------------- | ------------------------------------------------------------------------------------ |
| Exclusions in Microsoft Defender for Identity | [MDI Exclusions](https://learn.microsoft.com/en-us/defender-for-identity/exclusions) |
|                                               |                                                                                      |



Microsoft Defender offers various built in Detection Rules. This Rules also alert you for valid scenarios, for example Domain Controllers doing dcsyn or Accounts running remote code. You can exclude this users, devices and ip adresses from specific rules or from all the rules. Here is how: 

<br>

## Exclusions in the Microsoft 365 Defender Portal

### Exclusions by Rule
Navigate to: <br>
[Microsoft 365 Defender portal](security.microsoft.com) -> Settings -> Identities -> Excluded Entities -> Exclusions by detection rule

Select the Rule, you want to add Exclusions. You have the following options:

![Exclusion Options](/img/posts/20230105/ExcludeIdentities.png)

Select the Entities you want to exclude and click save


Confirm that the newly added Entities show up in the Overview

![Exclusions Overview](/img/posts/20230105/Overview.png)

The newly added Entities should be excluded in future alerts. 

<br>

### Global Exclusions

Navigate to: <br>
[Microsoft 365 Defender portal](security.microsoft.com) -> Settings -> Identities -> Excluded Entities -> Global Excluded Entities

Add Entities here, that should be excluded from all Defender Identity Alerts. 

<br><br>

## Exclusions in the Defender for Identity Portal

Navigate to: <br>
[Microsoft Defender for Identity portal](portal.atp.microsoft.com) -> Settings -> Exclusions

Add the Entities to the specific Rules to exclude them from future Alerts.

![Exclusions Overview](/img/posts/20230105/ExclusionsMDI.png)

