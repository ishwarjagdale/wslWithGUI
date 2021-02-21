# wslWithGUI
---
Run Ubuntu Desktop GUI on Windows Subsystem Linux 2 on Windows 10
---
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

---
### Step 2: Update to Windows Subsystem Linux
Download WSL2 Update Package: [Download Package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

**Now Set WSL default to version 2 using the following command**
In CMD or Powershell
```cmd
wsl --set-default-version 2
```

Now, if everything done correctly wsl will be updated and set default for linux installations
---
### Step 3: Install Ubuntu
Download the LTS version of Ubuntu from the Microsoft Store : [Link](https://www.microsoft.com/store/productId/9N6SVWS3RX71)

After downloading, open the Ubuntu app it'll install the linux subsystem.
Follow the instructions and enter your unix username and password, when the linux is setup install the updates the system.
```sh
sudo apt install update && sudo apt upgrade
```
---
### Step 4: Install xrdp service and Ubuntu Gnome Desktop
We'll be using the Remote Desktop Protocol to connect to the display

```sh
sudo apt install xrdp gnome-shell-desktop
```
During installation if prompted to configure display manager, select ```gdm```

---
### Step 5: Configure XRDP
- Take a backup of the xrdp first
```sh
sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
```
- Change the default rdp port to 3390 (optional)
```sh
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
```
- Change the resolution for better quality (optional)

*The rdp connection will be local so why not better image quality*
```sh
sudo sed -i 's/max_bpp=32/#max_bpp=32\nmax_bpp=128/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/xserverbpp=24/#xserverbpp=24\nxserverbpp=128/g' /etc/xrdp/xrdp.ini
```
- Edit the xrdp window manager
```sh
sudo nano /etc/xrdp/startwm.sh
```
After opening the file go to the end of the file and comment out the last two lines like this and
```gnome-session``` under it.
```sh
# test -x /etc/X11/Xsession && exec /etc/X11/Xsession
# exec /bin/sh /etc/X11/Xsession
gnome-session
```
---
### Step 6: Install the ubuntu-systemd script 
Clone the git repo given below and run it [Link to Repo](https://github.com/DamionGans/ubuntu-wsl2-systemd-script.git)
```sh
git clone https://github.com/DamionGans/ubuntu-wsl2-systemd-script.git
cd ubuntu-wsl2-systemd-script/
bash ubuntu-wsl2-systemd-script.sh
# Enter your password and wait until the script has finished
```
After that exit the shell using ```exit``` command, 
and restart the wsl using  
```
wsl --shutdown
```
then
```
wsl
```
in CMD or PowerShell

---
## Done!!
### Now run the xrdp service using (in shell)
```sh
sudo /etc/init.d/xrdp start
```
### Open Windows Remote Desktop Service
search for rdp in start menu

Use Computer as : ```localhost:3390``` or ```localhost:3389``` if you didn't change the port.

Then click Connect

You'll be asked for the unix username and password and keep the session type to xorg

---
That's it.
Thank you for reading!
