# My Manajro KDE installation

# Setting
*  Kernel: Install latest and restart
*  Hardware Configuration: Auto install proprietary driver and restart
*  Language packages: Install packages
*  Time and Date --> Hardware clock in local timezone: true
*  Workspace Behavior --> General Behavior --> Animation speed: Instant
*  Workspace Behavior --> General Behavior --> Click behavior: Double click
*  Workspace Behavior --> Desktop Effect --> Remove Screen Edge
*  Workspace Behavior --> Screen Edges --> No
*  Workspace Behavior --> Screen locking --> Lock screen: off
*  Shortcut --> Global Shortcut --> Defaults
*  Shortcut --> Global Shortcut --> Krunner: alt+f2
*  Shortcut --> Global Shortcut --> KWin --> Hide window boder: Meta+Enter
*  Shortcut --> Global Shortcut --> KWin --> Maximum window: Meta+PageUp
*  Shortcut --> Global Shortcut --> KWin --> Minimum window: Meta+PageDown
*  Shortcut --> Global Shortcut --> KWin --> Toggle Present Windows (Current Desktop): Meta+Tab
*  Shortcut --> Global Shortcut --> Yakuake: window+f12
*  Startup and Shutdown --> Autostart --> Add program: KSysGuard
*  Regional Setting --> Language: English
*  Regional Settings --> Formats --> Region: Viet Nam
*  Regional Settings --> Formats --> Detail Setting --> Number: Default
*  Regional Settings --> Formats --> Detail Setting --> Currency: Default
*  Input Devices --> Keyboard --> Numlock: On
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
```
```bash
Enable AUR support: true
Check update from AUR: true
```

# NVIDIA drivers (optional)
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

GUI (or use pamac install --no-confirm)
optimus-manager-qt

Add auto-start optimus-manager-qt
Restart
```

- [Guide: Install and configure optimus-manager for hybrid GPU setups (Intel/NVIDIA)](https://forum.manjaro.org/t/guide-install-and-configure-optimus-manager-for-hybrid-gpu-setups-intel-nvidia/92196)

# Fix KDE bug
```bash
sudo nano /usr/lib/NetworkManager/conf.d/20-connectivity.conf
```
```bash
[connectivity]
#uri=http://www.archlinux.org/check_network_status.txt
uri=http://networkcheck.kde.org/
```
- [Log in required for ethernet at home?”](https://www.reddit.com/r/ManjaroLinux/comments/keabph/log_in_required_for_ethernet_at_home/)

# Disable PC Speaker
```bash
sudo rmmod pcspkr
sudo nano /etc/modprobe.d/nobeep.conf
```
```bash
# Do not load the 'pcspkr' module on boot.
blacklist pcspkr
```

# Automount partition
```bash
sudo mkdir /mnt/disk1
sudo mkdir /mnt/disk2
sudo mkdir /mnt/disk3
sudo blkid /dev/sdb5
sudo blkid /dev/sda1
sudo blkid /dev/sda2
sudo nano /etc/fstab
```
```bash
UUID=01D5AFE0E284B260   /mnt/disk1  ntfs    defaults        0 0
UUID=01D5308C5EDFFD30   /mnt/disk2  ntfs    defaults        0 0
UUID=01D5308C6B0D0DF0   /mnt/disk3  ntfs    defaults        0 0
```

# Add swap
```bash
sudo fallocate -l 4G /swapfile
sudo mkswap /swapfile
sudo chmod u=rw,go= /swapfile
sudo swapon /swapfile
sudo bash -c "echo /swapfile none swap defaults 0 0 >> /etc/fstab"
```

# SDDM Auto numlock
```bash
sudo nano /etc/sddm.conf

Numlock=on
```

# Apps
```bash
GUI (or use pamac install --no-confirm)

yay-bin
google-chrome
vivaldi
psensor
gnome-keyring
skypeforlinux-stable-bin
telegram
caprine
clementine
mpv
Celluloid
Calibre
Stellarium
GIMP
KRDC
Krfb
Grub Customizer
Kvantum-manjaro
kdialog
Piper
neofetch
subtitleeditor
```

# IDE & Compiler

# Git
```bash
GUI (or use pamac install --no-confirm)

gitflow-avh
gitkraken
```
```bash
git config --global user.name "Duc Tran"
git config --global user.email tv.duc95@gmail.com
git config --global core.askpass /usr/bin/ksshaskpass
```
*  Optional: use ksshaskpass
```bash
sudo nano ~/.config/autostart-scripts/ssh-add.sh
#!/bin/sh
ssh-add -q < /dev/null

sudo nano ~/.config/plasma-workspace/env/askpass.sh
#!/bin/sh
export SSH_ASKPASS='/usr/bin/ksshaskpass'
export GIT_ASKPASS='/usr/bin/ksshaskpass'
```
```bash
Crack GitKraken

npm i
npm run-script build
sudo node dist/bin/gitcracken.js patcher
```
- [GitCracken](https://github.com/5cr1pt/GitCracken)

# C++
```bash
GUI (or use pamac install --no-confirm)

gcc
clang
```

# Go
```bash
GUI (or use pamac install --no-confirm)

go
```

# Java
```bash
GUI (or use pamac install --no-confirm)

jdk-openjdk
```

# .NET Core
```bash
GUI (or use pamac install --no-confirm)

dotnet-sdk
aspnet-runtime
```
```bash
Install .NET Core 3.1

sudo chmod 777 dotnet-install.sh
sudo ./dotnet-install.sh --channel 3.1 --install-dir /usr/share/dotnet
```
- [dotnet-install scripts](https://dot.net/v1/dotnet-install.sh)
```bash
dotnet tool install --global dotnet-ef
sudo nano ~/.xprofile

export PATH="$PATH:/home/ductran/.dotnet/tools"
```

# Nodejs
```bash
GUI (or use pamac install --no-confirm)

nodejs
npm
(or sudo pacman -S nodejs npm)
```
```bash
sudo rm -rfv /etc/sysctl.d/*
echo "fs.inotify.max_user_watches=524288" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p

sudo npm install -g @angular/cli
```
- [Install NodeJS via package manager](https://nodejs.org/en/download/package-manager/#arch-linux)

# MariaDB
```bash
GUI (or use pamac install --no-confirm)

mariadb
```
```bash
sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
sudo systemctl start mariadb
sudo mysql_secure_installation
```
- [MariaDB - ArchWiki](https://wiki.archlinux.org/index.php/MariaDB)

# PostgreSQL
```bash
GUI (or use pamac install --no-confirm)
https://askubuntu.com/questions/736638/fcitx-wont-trigger-ime-on-superspace
postgresql
pgadmin4
```
```bash
sudo su postgres -l
initdb --locale=en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data
exit
sudo systemctl start postgresql
sudo su postgres -l
createuser --interactive --pwprompt
exit
sudo systemctl stop postgresql
```
- [PostgreSQL - ArchWiki](https://wiki.archlinux.org/index.php/PostgreSQL)

# VSCode
```bash
GUI (or use pamac install --no-confirm)

visual-studio-code-bin
```

# Codeblocks
```bash
GUI (or use pamac install --no-confirm)

Codeblocks
```

# Jetbrains
```bash
GUI (or use pamac install --no-confirm)

webstorm
intellij-idea-ultimate-edition
rider
datagrip
clion
goland

Note: edit rider PKGBUILD _installdir='/opt'
```
```bash
sudo ark -b -o /opt /mnt/disk3/Software/IDE/java-11.0.7-jetbrain.zip
sudo mv /opt/java-11.0.7-jetbrain /opt/jbr
```
```bash
sudo nano /opt/datagrip/bin/datagrip.sh
export DATAGRIP_JDK=/opt/jbr

sudo nano /opt/intellij-idea-ultimate-edition/bin/idea.sh
export IDEA_JDK=/opt/jbr

sudo nano /opt/rider/bin/rider.sh
export RIDER_JDK=/opt/jbr

sudo nano /opt/webstorm/bin/webstorm.sh
export WEBIDE_JDK=/opt/jbr
```
or
```bash
sudo nano ~/.xprofile

export DATAGRIP_JDK=/opt/jbr
export IDEA_JDK=/opt/jbr
export RIDER_JDK=/opt/jbr
export WEBIDE_JDK=/opt/jbr
export CLION_JDK=/opt/jbr
export GOLAND_JDK=/opt/jbr
```

# Redis
```bash
GUI (or use pamac install --no-confirm)

redis
```

# RabbitMQ
```bash
GUI (or use pamac install --no-confirm)

RabbitMQ
```

# Apache
```bash
GUI (or use pamac install --no-confirm)

apache
```

# Nginx
```bash
GUI (or use pamac install --no-confirm)

nginx
```
```bash
sudo mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
sudo mkdir /etc/nginx/conf.d
sudo cp ~/Downloads/nginx.conf /etc/nginx/nginx.conf
sudo cp ~/Downloads/127.0.0.1.conf /etc/nginx/conf.d/127.0.0.1.conf
```

# FTP Server
```bash
GUI (or use pamac install --no-confirm)

bftpd
```
```bash
sudo nano /etc/bftpd.conf

ANONYMOUS_USER="yes"
DENY_LOGIN="no"
```

# Browser intergation
```bash
GUI (or use pamac install --no-confirm)

plasma-browser-integration
```

# Fcitx
```bash
GUI (or use pamac install --no-confirm)

fcitx5
fcitx5-gtk fcitx5-qt
fcitx5-chinese-addons fcitx5-unikey
fcitx5-configtool
```
```bash
sudo nano ~/.xprofile

export INPUT_METHOD=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```
- [fcitx shortcut](https://askubuntu.com/questions/736638/fcitx-wont-trigger-ime-on-superspace)

# Tweaks
*  Unpin all app in task bar
*  Configure desktop --> Tweak --> Show the desktop toolbox: off
*  Configure appplication laucher --> Show application by name: on
*  Pin favorite apps: System Settings, Add or Remove Software, Dolphin, Vivaldi, Chrome, Firefox, Skype, Visual Studio Code, Webstorm
*  Configure Panel --> Screen Edge: Left
*  Edit panel --> Add widget --> Download new widget: Win7 volume mixer
*  Configure System Tray --> Extra items: clipboard, Device notifier, Display Configuration, KDE Connect, Media Player, Notification, Printer, Weather report
*  Configure System Tray --> Entries --> Hidden all
*  Configure System Tray --> Entries --> Auto: Notification, psensor, Clipboard
*  Edit panel --> Add widget: Battery, Volume mixer, Network, Bluetooth, Touchpad, Input Method panel
*  Input Method panel --> Hide: fcitx, virtual keyboard, Telex, Unicode, Half width, Spell check, Macro, Full width input, No remind
*  Edit panel --> More Setting --> Auto hide
*  Lock widget

# Theme
*  Global theme: Nordian Global
*  GTK Theme: Nordian Breeze GTK
*  Icon: Breeze Nordian
*  SDDM: Nordian
*  Application Style: kvantum
*  Kvantum: Nordian Kvantum
*  Wallpaper: Plasma Desktop Wallpaper 1591

# Theme 2
*  Global theme: Arc KDE
*  GTK Theme: Plane GTK Arc Dark
*  Icon: papirus dark
*  SDDM: KDE-Story
*  Application Style: kvantum
*  Kvantum: Arc Dark

# Windows Font
```bash
mkdir /usr/share/fonts/WindowsFonts
cp /windows/Windows/Fonts/* /usr/share/fonts/WindowsFonts/
chmod 644 /usr/share/fonts/WindowsFonts/*
fc-cache --force
```
- [Microsoft fonts](https://wiki.archlinux.org/index.php/Microsoft_fonts)
