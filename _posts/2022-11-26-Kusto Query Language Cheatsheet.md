---
title: Kusto Query Language Cheatsheet
date: 2022-11-26 14:00:00 +0000
categories: [KQL]
tags: [kusto query language, kql, cheatsheet]     # TAG names should always be lowercase
---

# KQL - Kusto Query Language

## Docs and Sources

| Description              | Link                                                                                                                                         |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Markdown Best Practices  | [Markdown Best Practices](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/best-practices)                                   |
| KQL QUick Reference      | [MS KQL Quick Reference](https://learn.microsoft.com/en-us/azure/data-explorer/kql-quick-reference)                                          |
| Visualization            | [MSLearn Chart Vizualization](https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-chart-visualizations)                |
| Defender Hunting Queries | [Github Defender Hunting Queries](https://github.com/microsoft/Microsoft-365-Defender-Hunting-Queries)                                       |
| Advanced Hunting Schema  | [MSLearn Table Schema](https://learn.microsoft.com/en-us/microsoft-365/security/defender/advanced-hunting-schema-tables?view=o365-worldwide) |





<br> <br>

---

## Most Used

| Operator   | Description                                  | Syntax                                                                                                |
| ---------- | -------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| take       | Print limited Amout of Rows                  | `SigninLogs \| take 100`                                                                              |
| where      | Filter on Condition                          | `SigninLogs \| where Identity has "giger"` <br> `SigninLogs \| where Identity == "giger@contoso.com"` |
| count      | Count Results                                | `SiginLogs \| where Country != "CH" \| count`                                                         |
| order by   | Sortieren nach                               | `project Users \| order by UserPrincipalName`                                                         |
| project    | Anzeigen gewisser Spalten                    | `SigninLogs \| project TimeGenerated, UserprincipalName, Location`                                    |
| extend     | Erweitern der Tabelle um eine weitere Spalte | `\| extend Status = tostring(Status.failureReason)`                                                   |
| distinct   | Filter duplicates                            | `Distinct Location`                                                                                   |
| summarize  | Resultate zählen nach Spaltenname            | `summarize Total = count() by <Spaltename>`                                                           |
| let        | Variable definieren, Resultate abspeichern   | `let resultate = SigninLogs \| where Identity == "gig"`                                               |
| search     | Durchsuchen aller Logs nach Stichwörtern     | `search "gig"`                                                                                        |
| union      | Tabellen zusammenführen                      | `union SigninLogs, AadNoninteractiveSigninlogs`                                                       |
| isnotempty | Alle leeren Felder rausfiltern               | `ExampleLogs \| where isnotempty(Spaltenname)`                                                        |
|            |                                              |                                                                                                       |

<br> <br>

## Operatoren

[String Operatoren](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/datatypes-string-operators#operators-on-strings)


[Numerical Operatoren](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/numoperators)

<br>
<br>

## Nützliche Queries

**Array definieren um Werte zu filtern**
```
let excludedAdresses = dynamic(["8.8.4.4", "8.8.8.8"]);
| where DestinationIP !in (excludedAdresses)
```

---

**Herausfiltern von gewissen Resultaten**
```
| where not(ResultType has_any ("10", "20"))
```

---

**Resultate zeitlich begrenzen**
```
Signinlogs | where Timegenerated > ago(1m)
Signinlogs | where Timegenerated > ago(1h)
Signinlogs | where Timegenerated > ago(1d)
Signinlogs | where Timegenerated > ago(1m)
```

---

**Resultate visualisieren**

[MSLearn](https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-chart-visualizations)

Charttypes: Areachart, Barcahrt, Columnchart, Linechart, Piechart, Scatterchart, ...

```
OfficeActivity
| summarize test = count() by Operation, bin(TimeGenerated, 4h)    #Generates 2 Axis
| render timechart      #Generates Graphics
```

**Logins visualisieren**
```
SigninLogs
| where Identity  has "gig"
| summarize x = count() by bin(TimeGenerated, 10m) 
| render timechart 
```

--- 

**Wert aus einer Subtabelle extrahieren**
```
| extend Status = tostring(Status.failureReason)

- Aus einem Array
| extend location = (todynamic(Entities)[2]).Location.City

- Aus XML Feld
| extend parsed = parse_xml(EventData)
```

---

**Externe Daten laden**

```
let IPList = externaldata(IPAddress:string)[@"https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Sample%20Data/Feeds/Log4j_IOC_List.csv"] with (format="csv", ignoreFirstRecord=True);
let IPRegex = '[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}\\.[0-9]{1,3}';
```

