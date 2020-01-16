---
layout: post
title: "Save credential XML file"
date: 2020-01-16 14:45
category: [powershell,windows]
---

```powershell
$Credential = Get-Credential
$Credential | Export-CliXml -Path "${env:\userprofile}\Jaap.Cred"
$Credential = Import-CliXml -Path "${env:\userprofile}\Jaap.Cred"
```
