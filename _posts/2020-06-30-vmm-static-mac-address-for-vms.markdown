---
title: VMM static MAC address for VMs
layout: 
category: [powershell,windows]
---

```powershell
$VMS = Get-SCVirtualMachine | Select -ExpandProperty VirtualNetworkAdapters | Where { $_.MACAddressType -eq "Dynamic" } | where Name -NotLike $env:COMPUTERNAME 

foreach ($VM in $VMS) { 
Get-SCVirtualMachine -Name $VM  | Stop-SCVirtualMachine -Shutdown 
$VirtualNetworkAdapter = Get-SCVirtualNetworkAdapter -VMMServer localhost -VM "$VM" 
Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $VirtualNetworkAdapter -MACAddress "00:00:00:00:00:00" -MACAddressType Static 
Start-SCVirtualMachine -VM $VM.Name
} 
```