## For win10 uncheck following features:
Hyper-V  
Virtual Mahine Platform  
Windows Hypervisor Platform  
Windows Sandbox  
## For win10 virtualbox
```
VBoxManage modifyvm <VirtualMachineName> --nested-hw-virt on
```
## Run this in the cmd as an Admin
```
bcdedit /set hypervisorlaunchtype off
```
### Turn it back on
```
bcdedit /set hypervisorlaunchtype auto
```
