## Ubuntu 22.04 Installation on laptop (i7, RTX 5060, Dual system with Win 11)
* Can't install Ubuntu 20.04 successfully (No wifi module detection, no SSD detection)
  
### Preparation
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

### Install Terminator
```
sudo apt-get install terminator
```

### Install Git
```
sudo apt install git
```

### Install ROS
