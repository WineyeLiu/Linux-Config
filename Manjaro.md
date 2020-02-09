# My Fedora KDE installation

# Setting
*  Kernel: Install latest and restart
*  Hardware Configuration: Auto install proprietary driver and restart
*  Language packages: Install packages
*  Time and Date --> Set time and date automatical: true
*  Time and Date --> Hardware clock in local timezone: true
*  Global Theme: Breeze Dark
*  Workspace Behavior --> General Behavior --> Click behavior: Double click
*  Workspace Behavior --> Screen Edges --> No
*  Workspace Behavior --> Screen locking --> Lock screen: off
*  Shortcut --> Global Shortcut --> Krunner: window+space
*  Shortcut --> Global Shortcut --> Krunner: alt+f2
*  Shortcut --> Global Shortcut --> Yakuake: window+f12
*  Startup and Shutdown --> Autostart --> Add program: KSysGuard
*  Startup and Shutdown --> Splash Screen: Breath
*  Regional Settings --> Formats --> Region: Viet Nam
*  Regional Settings --> Formats --> Detail Setting --> Number: Default
*  Regional Settings --> Formats --> Detail Setting --> Currency: Default
*  Input Devices --> Mouse --> Poiter speed: 3
*  Input Devices --> Touchpad --> Poiter speed: 3
*  Input Devices --> Touchpad --> Tapping --> Tap-to-click: true
*  Display and Monitor --> Compositor --> Animation speed: Instant
*  Display and Monitor --> Compositor --> Rendering backend: OpenGL 3.1
*  Power Management --> Energy Saving --> On AC Power --> Brightness: 100%
*  Power Management --> Energy Saving --> On AC Power --> Dim screen: 30 min
*  Power Management --> Energy Saving --> On AC Power --> Screen energy saving: 35 min
*  Power Management --> Energy Saving --> On AC Power --> When laptop lid close: Turn off screen
*  Power Management --> Energy Saving --> On AC Power --> Wireless: On
*  Power Management --> Energy Saving --> On Battery --> Brightness: 100%
*  Power Management --> Energy Saving --> On Battery --> Dim screen: 30 min
*  Power Management --> Energy Saving --> On Battery --> Screen energy saving: 35 min
*  Power Management --> Energy Saving --> On Battery --> Suspend session: Off
*  Power Management --> Energy Saving --> On Battery --> When laptop lid close: Turn off screen
*  Power Management --> Energy Saving --> On Battery --> Wireless: On
*  Power Management --> Energy Saving --> On Low Battery --> Brightness: 40%
*  Power Management --> Energy Saving --> On Low Battery --> Dim screen: 10 min
*  Power Management --> Energy Saving --> On Low Battery --> Screen energy saving: 15 min
*  Power Management --> Energy Saving --> On Low Battery --> Suspend session: 30 min
*  Power Management --> Advanced Settings --> At critical level: Shutdown

# Full system update
```bash
sudo pacman -Syu
sudo pacman -Syyu
```

# Add AUR Repository
```bash
Add or remove software
Preference

Enable AUR support: true
Check update from AUR: true
```

# NVIDIA drivers
```bash
sudo pacman -S optimus-manager
sudo systemctl disable bumblebeed.service
cd /etc/X11/xorg.conf.d/
ls -la
sudo mv 90-mhwd.conf 90-mhwd.conf.bak
cd /etc/X11/
ls -la
sudo nano /etc/sddm.conf
put a # before the line starting with 'DisplayCommand and 'DisplayStopCommand'
pamac install optimus-manager-qt
Add auto-start optimus-manager-qt
Restart
```

- [Guide: Install and configure optimus-manager for hybrid GPU setups (Intel/NVIDIA)](https://forum.manjaro.org/t/guide-install-and-configure-optimus-manager-for-hybrid-gpu-setups-intel-nvidia/92196)
