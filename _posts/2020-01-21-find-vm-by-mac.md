---
layout: post
title: VmWare find vm by mac address
date: 2020-01-21 05:55
category: [vmware,powershell]
---

PowerCLI

```powershell
Get-VM | Get-NetworkAdapter | Where {$_.MacAddress -eq "00:50:56:a2:fe:99"} | Format-List
```
