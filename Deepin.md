# My Deepin installation

# Setting
*  Display scaling: 1.0
*  Transparency: 4
*  Plugged in --> Monitor suspend: 30
*  Plugged in --> Computer suspend: Never
*  Plugged in --> Suspend on lid close: Off
*  On battery --> Monitor suspend: 30
*  On battery --> Computer suspend: Never
*  On battery --> Suspend on lid close: Off
*  Password require to wake up monitor: Off
*  Mouse --> Pointer speed: 2
*  Touch pad --> Pointer speed: 2
*  Regional Setting --> Format --> Currency: Default
*  Input Devices --> Mouse --> Pointer speed: 4, flat
*  Input Devices --> Touch pad --> Tap to click: On

# Full system update
```bash
sudo apt-get update
sudo apt-get upgrade
```

# Config iw wifi
```bash
sudo nano /etc/modprobe.d/iwlwifi.conf
options iwlwifi bt_coex_active=0 power_save=0 swcrypto=0
```

# Update graphic driver
```bash
Graphic Driver Manager: bumblebee
```
