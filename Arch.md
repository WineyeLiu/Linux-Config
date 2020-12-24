# My Arch KDE installation
[Installation guide](https://wiki.archlinux.org/index.php/Installation_guide)
[KDE](https://wiki.archlinux.org/index.php/KDE#Installation)

# Boot Arch
*  Boot Arch Linux (x86_64)

# Connect to Internet
```bash
iwctl
device list
station device scan
station device get-networks
station device connect SSID
```
* or use
```bash
iwctl --passphrase passphrase station device connect SSID
```

# Update the system clock
```bash
timedatectl set-timezone Asia/Ho_Chi_Minh
timedatectl set-ntp true
```

# Update pacman, set mirror
```bash
pacman -Syyy
```
* optional
```bash
pacman -S python
pacman -S reflector
reflector -c Singapore -a 6 --sort rate --save /etc/pacman.d/mirrorlist
pacman -Syyy
```

# Partition the disks
```bash
lsblk
cfdisk /dev/sda
```
* Choose Free space  
  Enter New  
  Then Write  
  Quit  
* Verify new partition:
```bash
lsblk
mkfs.ext4 /dev/sda6
lsblk
```

# Mount the file systems
```bash
mount /dev/sda6 /mnt
lsblk
```
* Optional: mount windows 10
```bash
mkdir /mnt/windows10
mount /dev/sda3 /mnt/windows10
```

# Install Linux
```bash
pacstrap /mnt base linux linux-firmware nano intel-ucode
```

# Configure the system
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

# Chroot
```bash
arch-chroot /mnt
```

# Swapfile
```bash
fallocate -l 4G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```
```bash
nano /etc/fstab

/swapfile none swap defaults 0 0
```

# Time zone
* List timezones
```bash
timedatectl list-timezones
```
```bash
ln -sf /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime
hwclock --systohc
```

# Localization
```bash
nano /etc/locale.gen

uncommnet en_US.UTF-8 UTF-8
```
```bash
locale-gen
echo "LANG=en_US.UTF-8" >> /etc/locale.conf
```

# Network configuration
```bash
nano /etc/hostname

delllatitude6530
```
```bash
nano /etc/hosts

127.0.0.1	localhost
::1		localhost
127.0.1.1	delllatitude6530.localdomain	delllatitude6530
```

# Root password
```bash
passwd
```

# GRUB and others
```bash
pacman -S grub efibootmgr os-prober ntfs-3g networkmanager network-manager-applet wpa_supplicant dialog mtools dosfstools base-devel linux-headers git bluez bluez-utils pulseaudio-bluetooth cups openssh
```
```bash
mkdir /boot/EFI
mount /dev/sda1 /boot/EFI
grub-install --target=x86_64-efi --efi-directory=/boot/EFI --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

# Services
```bash
systemctl enable NetworkManager
systemctl enable bluetooth
systemctl enable cups
systemctl enable sshd
```
* optional
```bash
systemctl enable sshd
```

# User
```bash
useradd -m -g users -G wheel,storage,network,power ductran
passwd ductran
EDITOR=nano visudo

uncomment # %wheel ALL=(ALL) ALL
```

# Reboot
```bash
exit
umount -a
reboot
```

# Connect to internet
```bash
ip a
nmtui
```

# Xorg
```bash
pacman -S xorg
```

# Enable multilib
```bash
nano /etc/pacman.conf

uncomment
#[multilib]
#Include = /etc/pacman.d/mirrorlist
```

# Graphic driver
```bash
pacman -S xf86-video-intel xf86-video-amdgpu xf86-video-nouveau mesa lib32-mesa
pacman -S vulkan-intel lib32-vulkan-intel vulkan-radeon lib32-vulkan-radeon
```
* For nvidia latest driver
```bash
pacman -S nvidia nvidia-utils lib32-nvidia-utils
```

# Sound driver
```bash
pacman -S alsa-firmware alsa-utils alsa-lib alsa-plugins alsa-oss lib32-alsa-lib lib32-alsa-oss lib32-alsa-plugins
pacman -S pulseaudio pulseaudio-alsa pulseaudio-equalizer
```

# Input driver
```bash
pacman -S xf86-input-elographics xf86-input-evdev xf86-input-libinput xf86-input-void
```

# SDDM
```bash
pacman -S sddm
systemctl enable sddm
```

# KDE Plasma
```bash
pacman -S plasma plasma-wayland-session kde-applications
```

# Libre Office
```bash
pacman -S libreoffice
```

# Browser
```bash
pacman -S thunderbird firefox
```

# Git
```bash
pacman -S git
```

# Reboot
```bash
reboot
```

# Yay (optional)
```bash
git clone https://aur.archlinux.org/yay-bin.git
cd yay-bin/
makepkg -si PKGBUILD
```

# Pamac
```bash
git clone https://aur.archlinux.org/pamac-aur.git
cd pamac-aur/
makepkg -si PKGBUILD
```

# Install Nvidia 390
```bash
pamac install nvidia-390xx 	nvidia-390xx-utils lib32-nvidia-390xx-utils
```

# Install Bumblebee
```bash
pacman -S bumblebee
```

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


# Disable PC Speaker
```bash
sudo rmmod pcspkr
sudo nano /etc/modprobe.d/nobeep.conf
```
```bash
# Do not load the 'pcspkr' module on boot.
blacklist pcspkr
```

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

# Apps
```bash
GUI (or use pamac install --no-confirm)

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
vlc
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
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
exit
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
```
```bash
sudo cp /opt/webstorm/bin/webstorm.png /usr/share/icons/hicolor/128x128/apps/webstorm.png
sudo cp /opt/datagrip/bin/datagrip.png /usr/share/icons/hicolor/128x128/apps/datagrip.png
sudo nano /usr/share/applications/jetbrains-datagrip.desktop
sudo nano /usr/share/applications/jetbrains-webstorm.desktop
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

# SDDM Auto numlock
```bash
sudo nano /etc/sddm.conf

Numlock=on
```

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
