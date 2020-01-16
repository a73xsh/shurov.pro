---
layout: post
title: "Recovery vCenter service after recover from backup"
date: 2020-01-16 14:51
category: [vmware]
---

Start all services

```bash
# Start services or Reboot  
service-control --start --all
```
If start failed

```bash
20-01-15T12:14:34.388Z   RC = 1
Stdout =
Stderr = Failed to execute operation: Unit file is masked

2020-01-15T12:14:34.389Z   {
    "resolution": null,
    "detail": [
        {
            "args": [
                "Stderr: Failed to execute operation: Unit file is masked\n"
            ],
            "id": "install.ciscommon.command.errinvoke",
            "localized": "An error occurred while invoking external command : 'Stderr: Failed to execute operation: Unit file is masked\n'",
            "translatable": "An error occurred while invoking external command : '%(0)s'"
        }
    ],
    "componentKey": null,
    "problemId": null
}
2020-01-15T12:14:34.389Z   Running command: ['/usr/bin/systemctl', 'unset-environment', 'VMON_PROFILE']
2020-01-15T12:14:34.391Z   Done running command
Service-control failed. Error {
    "resolution": null,
    "detail": [
        {
            "args": [
                "vmware-vmon"
            ],
            "id": "install.ciscommon.service.failstart",
            "localized": "An error occurred while starting service 'vmware-vmon'",
            "translatable": "An error occurred while starting service '%(0)s'"
        }
    ],
    "componentKey": null,
    "problemId": null
}
```

recover services

```bash
# List all disabled services for removal.   
find /etc/systemd/system/ -lname '/dev/null' -exec ls {} \;    
# Automatically remove them (or rm each file)  
find /etc/systemd/system/ -lname '/dev/null' -exec rm {} \;   
# Relaod systemctl daemon  
systemctl daemon-reload   
  
# Start services or Reboot  
service-control --start --all  
```

if services cannot start
https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.install.doc/GUID-D3BA6EB6-7BD9-44E5-8A6E-7C2CE7808630_copy3.html

```bash
vcenter-restore -u psc_administrator_username -p psc_administrator_password 
```
