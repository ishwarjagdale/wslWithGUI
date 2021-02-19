# wslWithGUI

Run Ubuntu Desktop GUI on Windows Subsystem Linux 2 on Windows 10

### Step 1: Activate Windows Subsystem Linux Feature
Open Powershell or CMD as administrator:
- Enable WSL Feature
```sh
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
- Enable Virtualization
```sh
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
Restart your device if needed, and make sure virtualization is enabled from bios

### Step 2: Update to Windows Subsystem Linux
Download WSL2 Update Package: [Download Package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

---
# Under Construction
