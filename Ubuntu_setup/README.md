# Ubuntu 22.04 Installation on laptop (i7, RTX 5060, Dual system with Win 11)
* Can't install Ubuntu 20.04 successfully (No wifi module detection, no SSD detection)
  
## Preparation
1. Prepare an Ubuntu 22.04 installation USB by [Rufus](https://rufus.ie/downloads/)
2. Shrink partition on a SSD on Win 11
3. Change boot order to USB in BIOS
4. Install Ubuntu
   
### Solve low resolution e.g. 800x600 (can't see buttons on installation window)
1. Turn off "bitlocker" in Windows 11
2. Turn off "security boot" in BIOS

### Solve Wifi detection (can't see wifi and bluetooth options in setting)
1. Download latest version of [Ubuntu 22.04](https://releases.ubuntu.com/jammy/) and re-prepare an Ubuntu installation USB
2. Re-do the steps in [Preparation](#preparation)

## Install Terminator
```
sudo apt-get install terminator
```

## Install Git
```
sudo apt install git
```

## Install NVIDIA driver
### 1. Install gcc-12
```bash
sudo apt install --reinstall gcc-12
sudo ln -s -f /usr/bin/gcc-12 /usr/bin/gcc
gcc --version
```

### 2. Block nouveau
```bash
sudo gedit /etc/modprobe.d/blacklist.conf
```

Open blacklist.conf, input the following commands after its original commands.
```bash
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```

Update 
```bash
sudo update-initramfs -u
```

Check whether successfully block nouveau or not
```bash
lsmod | grep nouveau
```
Nothing should be shown if nouveau is successfully blocked.

###3. Download driver from Nnidia

### 4. Update system
```bash
sudo apt update
sudo apt upgrade -y
```

### 5. Install
```bash
sudo apt install -y build-essential cmake
sudo apt install -y lightdm
```
Choose "lightdm"

### 6. Enter tty by pressing "ctrl + alt + f3"
   
### 7. Enter Ubuntu user name and password
   
### 8. Close GUI
```bash
sudo service lightdm stop
```

### 9. Install Nvidia driver
```bash
cd Downloads # location of driver
chmod 755 NVIDIA-Linux-86_64-570.169.run #press tab to see the driver name
sudo ./NVIDIA-Linux-x86_64-570.169.run -no-x-check -no-nouveau-check
```
*Multiple kernel module types are available for this systems. Which would you like to use?* --> MIT/GPL --> "Continue installation" --> "Continue installation"

*Install NVIDIA's 32-bit compatibility libraries?* --> NO

*Would you like to run the nvidia-xconfig utility to automatically update you X configuration file so that the NVIDIA X driver will be used when you restart X? Any pre-existing X configuration file will be backed up.* --> YES

If the Nvidia driver is successfully installed, then the following text is shown:

*Your X configuration file has been successfully updated. Installation of the NVIDIA Accelerated Graphics Driver for Linux-x86_64 (version:535.113.01) is now complete.*

Check driver version
```bash
nvidia-smi
```

Reboot
```bash
sudo service lightdm start && reboot
```

## [NVIDIA Driver Issue] If the Ubuntu GUI remains black after rebooting, try (thx to ChatGPT)
### 1. Disable Secure Boot in BIOS.

### 2. Install nvidia-prime (if not yet installed)
```
sudo apt install nvidia-prime
```
Then set to NVIDIA:
```bash
sudo prime-select nvidia
sudo reboot
```

### 3. Ensure NVIDIA kernel modules are loaded
```bash
lsmod | grep nvidia
```
We should see multiple entries like:
```
nvidia_uvm
nvidia_drm
nvidia_modeset
nvidia
```
If nothing appears, load them manually:
```bash
sudo modprobe nvidia
```
Then, re-check with 
```bash
lsmod | grep nvidia
```

### 4. If you input
```
prime-select query
```
and it shows
```
on-demand
```
Please ensure you finish step 2.

### 5. Force use of Xorg (disable Wayland completely)
   
Edit GDM configuration:
```bash
sudo nano /etc/gdm3/custom.conf
```
Ensure these lines are set:
```bash
WaylandEnable=false
```
Uncomment it if commented. Save with Ctrl+O, Enter, Ctrl+X.

Then reboot:
```bash
sudo systemctl restart gdm3
```
or
```bash
reboot
```

### 6. Regenerate Xorg configuration for NVIDIA
```bash
sudo nvidia-xconfig
sudo reboot
```

### 7. Set NVIDIA DRM kernel modeset
Ensure your GRUB config enables modeset.
```bash
sudo nano /etc/default/grub
```
Find:
```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```
Change to:
```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvidia-drm.modeset=1"
```
Save and update GRUB:
```bash
sudo update-grub
sudo reboot
```

### 8. Check your display manager (GDM vs LightDM)
   
If using GDM3, sometimes switching to LightDM fixes black screen issues:
```bash
sudo apt install lightdm
sudo dpkg-reconfigure lightdm
```
Select LightDM as default. 

Reboot:
```
sudo reboot
```
## Fix Incorrect Windows Time In Linux Dual Boot
```bash
timedatectl
```
We can see *RTC in local TZ: **no***

```bash
timedatectl set-local-rtc 1 --adjust-system-clock
timedatectl
```
Then we can see *RTC in local TZ: **yes***


