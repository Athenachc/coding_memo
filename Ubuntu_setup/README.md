## Ubuntu 20.04 Installation on laptop (i7, RTX 5060, Dual system with Win 11)
### Preparation
1. Prepare an Ubuntu 20.04 installation USB
2. Shrink partition on a SSD on Win 11
3. Change boot order to USB in BIOS
4. Install Ubuntu
   
### Solve low resolution e.g. 800x600 (can't see buttons on installation window)
1. Turn off "bitlocker" in Windows 11
2. Turn off "security boot" in BIOS

### Install Terminator
```
sudo apt-get install terminator
```

### Install Git
```
sudo apt install git
```

### Install ROS
