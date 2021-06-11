# My Legion 5 Arch KDE installation
[Installation guide](https://wiki.archlinux.org/index.php/Installation_guide)
[KDE](https://wiki.archlinux.org/index.php/KDE#Installation)

# Boot Arch
*  Boot Arch Linux (x86_64)

# Connect to Internet
```bash
iwctl
device list
iwctl adapter phy0 set-properties Powered on
station wlan0 scan
station wlan0 get-networks
station wlan0 connect SSID
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
pacman -S reflector
reflector -c Singapore -a 6 --sort rate --save /etc/pacman.d/mirrorlist
pacman -Syyy
```

# Partition the disks
```bash
lsblk
cfdisk /dev/nvmen1
```
* Choose Free space  
  Enter New  
  Then Write  
  Quit  
* Verify new partition:
```bash
lsblk
mkfs.ext4 /dev/nvmen1p3
lsblk
```

# Mount the file systems
```bash
mount /dev/nvmen1p3 /mnt
lsblk
```

# Install Linux
```bash
pacstrap /mnt base linux linux-firmware linux-headers nano amd-ucode
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
fallocate -l 8G /swapfile
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
hwclock --systohc --localtime
```

# Localization
```bash
nano /etc/locale.gen

uncomment en_US.UTF-8 UTF-8 vi_VN UTF-8
```
```bash
locale-gen
echo "LANG=en_US.UTF-8" >> /etc/locale.conf
```

# Network configuration
```bash
nano /etc/hostname

legion5
```
```bash
nano /etc/hosts

127.0.0.1	localhost
::1		localhost
127.0.1.1	legion5.localdomain	legion5
```

# Root password
```bash
passwd
```

# GRUB and others
```bash
pacman -S grub efibootmgr os-prober ntfs-3g networkmanager network-manager-applet wpa_supplicant dialog mtools dosfstools base-devel bluez bluez-utils openssh sshfs
```
```bash
mkdir /boot/EFI
mount /dev/nvmen1p2 /boot/EFI
grub-install --target=x86_64-efi --efi-directory=/boot/EFI --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

# Services
```bash
systemctl enable NetworkManager
systemctl enable bluetooth
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
pacman -S xf86-video-amdgpu xf86-video-nouveau mesa
pacman -S vulkan-radeon
pacman -S nvidia nvidia-utils nvidia-settings
```

# Sound driver
```bash
pacman -S alsa-firmware alsa-utils alsa-lib alsa-plugins alsa-oss
pacman -S pulseaudio pulseaudio-alsa pulseaudio-bluetooth pulseaudio-equalizer
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
pacman -S plasma plasma-wayland-session plasma-wayland-protocols sddm-kcm
pacman -S kde-graphics
pacman -S kde-multimedia
pacman -S kde-system
pacman -S kde-utilities
pacman -S kdepim
pacman -S kdesdk
pacman -S --needed kde-applications
```
or
```bash
pacman -S kde-applications
```

# Libre Office
```bash
pacman -S libreoffice-fresh
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
yay --editmenu --nodiffmenu --save
```

# Pamac
```bash
git clone https://aur.archlinux.org/pamac-aur.git
cd pamac-aur/
makepkg -si PKGBUILD
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

# Full system update
```bash
sudo pacman -Syu
sudo pacman -Syyu
```

# Update mirrorlist
```bash
sudo pacman -S reflector
sudo reflector --country Singapore --country Japan --country China --country HongKong --country 'South Korea' --country Vietnam  --country Germany --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

# NVIDIA Optimus (optional)
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

# Setting
*  Workspace Behavior --> General Behavior --> Animation speed: Instant
*  Workspace Behavior --> General Behavior --> Click behavior: Double click
*  Workspace Behavior --> Desktop Effect --> Remove Screen Edge
*  Workspace Behavior --> Screen Edges --> No
*  Workspace Behavior --> Screen locking --> Lock screen: off
*  Shortcut --> Global Shortcut --> Defaults
*  Shortcut --> Global Shortcut --> Import Windows cheme with win key
*  Shortcut --> Global Shortcut --> Krunner: untick alt+f2
*  Shortcut --> Global Shortcut --> KWin --> Hide window boder: Meta+Enter
*  Shortcut --> Global Shortcut --> KWin --> Maximum window: Meta+PageUp
*  Shortcut --> Global Shortcut --> KWin --> Minimum window: Meta+PageDown
*  Shortcut --> Global Shortcut --> KWin --> Toggle Present Windows (Current Desktop): Meta+Tab
*  Shortcut --> Global Shortcut --> Plasma --> Show desktop: untick Ctrl+F12
*  Shortcut --> Global Shortcut --> Yakuake: window+f12
*  Shortcut --> Global Shortcut --> Konsole: Ctrl+Alt+T
*  Startup and Shutdown --> Autostart --> Add program: Yakuake
*  Startup and Shutdown --> Autostart --> Add program: KSysGuard
*  Regional Setting --> Language: English
*  Regional Settings --> Formats --> Region: Viet Nam
*  Regional Settings --> Formats --> Detail Setting --> Number: Default
*  Regional Settings --> Formats --> Detail Setting --> Currency: Default
*  Input Devices --> Keyboard --> Numlock: On
*  Input Devices --> Mouse --> Poiter speed: 3
*  Input Devices --> Touchpad --> Poiter speed: 3
*  Input Devices --> Touchpad --> Tapping --> Tap-to-click: true
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

# Fix KDE bug
*  Fix check network bug
```bash
sudo nano /usr/lib/NetworkManager/conf.d/20-connectivity.conf
```
```bash
[connectivity]
#uri=http://www.archlinux.org/check_network_status.txt
uri=http://networkcheck.kde.org/
```
[Log in required for ethernet at home?”](https://www.reddit.com/r/ManjaroLinux/comments/keabph/log_in_required_for_ethernet_at_home/)
*  Fix shortcut bug
```bash
sudo nano ~/.config/plasma-org.kde.plasma.desktop-appletsrc
sudo nano ~/.config/kglobalshortcutsrc

Change Alt+F1 => Meta+Alt+F1
```

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
sudo blkid /dev/nvme0n1p3
sudo blkid /dev/nvme0n1p5
sudo blkid /dev/nvme1n1p1
sudo nano /etc/fstab
```
```bash
UUID=56F89722F896FF83   /mnt/disk1  ntfs    defaults        0 0
UUID=D4787282787262E2   /mnt/disk2  ntfs    defaults        0 0
UUID=74746E13746DD87E   /mnt/disk3  ntfs    defaults        0 0
```

# SDDM Auto numlock
```bash
sddm --example-config | sudo tee /etc/sddm.conf
sudo nano /etc/sddm.conf

Numlock=on
```

# Color Management
```bash
GUI (or use pamac install --no-confirm)

colord-kde
```

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
grub-customizer
kvantum-qt5
piper
vlc
qbittorrent
neofetch
htop
openvpn
networkmanager-openvpn
subtitleeditor
unrar
openssl
zenmonitor
motrix-bin
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
```
*  Optional: use keepassxc
```bash
git config --global credential.helper libsecret
```
*  Optional: use ksshaskpass
```bash
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

# C++
```bash
GUI (or use pamac install --no-confirm)

gcc
gdb
cmake
clang
llvm
lldb
lld
libc++
```

# Go
```bash
GUI (or use pamac install --no-confirm)

go
go-tools
```

# Java
```bash
GUI (or use pamac install --no-confirm)

jdk-openjdk
java-openjfx
jdk11-openjdk
java11-openjfx
```

# .NET Core
```bash
GUI (or use pamac install --no-confirm)

dotnet-sdk
aspnet-runtime
aspnet-targeting-pack
dotnet-sdk-3.1
aspnet-runtime-3.1
aspnet-targeting-pack-3.1
```
or
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

# Mono
```bash
GUI (or use pamac install --no-confirm)

mono
mono-tools
mono-addins
mono-msbuild
mono-msbuild-sdkresolver
xsp
```
config to run ASP .NET project
```bash
sudo mkdir /etc/mono/registry
sudo chmod uog+rw /etc/mono/registry

edit web.config
<dependentAssembly>
    <assemblyIdentity name="System.Net.Http" publicKeyToken="b03f5f7f11d50a3a" culture="neutral" />
    <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.2.0.0" />
</dependentAssembly>
```
- [Access to the path “/etc/mono/registry” is denied](https://stackoverflow.com/questions/24872394/access-to-the-path-etc-mono-registry-is-denied)
- [How to get Swashbuckle / Swagger working on the Mono (.NET) Framework?](https://stackoverflow.com/questions/36062557/how-to-get-swashbuckle-swagger-working-on-the-mono-net-framework)

# Nodejs
```bash
GUI (or use pamac install --no-confirm)

nodejs
npm

or

nvm
source /usr/share/nvm/init-nvm.sh
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.bashrc
nvm install node
nvm install --lts
```
```bash
sudo rm -rfv /etc/sysctl.d/*
echo "fs.inotify.max_user_watches=524288" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p

sudo npm install -g @angular/cli
```
- [Install NodeJS via package manager](https://nodejs.org/en/download/package-manager/#arch-linux)

# Android tools
```bash
GUI (or use pamac install --no-confirm)

android-tools
```

# Flutter
```bash
GUI (or use pamac install --no-confirm)

flutter
android-sdk
android-sdk-platform-tools
android-sdk-build-tools
android-sdk-cmdline-tools-latest
android-platform
```
```bash
sudo groupadd flutterusers
sudo gpasswd -a $USER flutterusers
sudo chown -R $USER:flutterusers /opt/flutter
sudo chmod -R g+w /opt/flutter/
```
```bash
sudo groupadd android-sdk
sudo gpasswd -a $USER android-sdk
sudo chown -R $USER:android-sdk /opt/android-sdk
sudo chmod -R g+w /opt/android-sdk
```
```bash
sudo nano ~/.xprofile

#Java
export JAVA_HOME='/usr/lib/jvm/java-14-openjdk/'

# Android SDK
export ANDROID_SDK_ROOT='/opt/android-sdk'
export PATH="$PATH:$ANDROID_SDK_ROOT/platform-tools/"
export PATH="$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin/"
export PATH="$PATH:$ANDROID_SDK_ROOT/tools/bin/"
export PATH="$PATH:$ANDROID_SDK_ROOT/tools/"

# Flutter
export PATH="$PATH:/opt/flutter/bin"
```
```bash
flutter doctor
flutter doctor --android-licenses
```

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

# MS SQL Server
```bash
GUI (or use pamac install --no-confirm)
mssql-server
```
```bash
sudo /opt/mssql/bin/mssql-conf setup
```
- [Installation guidance for SQL Server on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup?view=sql-server-ver15)

# VSCode
```bash
GUI (or use pamac install --no-confirm)

visual-studio-code-bin
```

# Codeblocks
```bash
GUI (or use pamac install --no-confirm)

codeblocks
```

# Jetbrains
```bash
GUI (or use pamac install --no-confirm)

webstorm
intellij-idea-ultimate-edition
datagrip
rider
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
cd Downloads/dotfiles/nginx
sudo cp nginx.conf /etc/nginx/nginx.conf
sudo cp 127.0.0.1.conf /etc/nginx/conf.d/127.0.0.1.conf
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

# PostMan
```bash
GUI (or use pamac install --no-confirm)

postman-bin
```

# Fcitx
```bash
GUI (or use pamac install --no-confirm)

fcitx5-im
fcitx5-chinese-addons fcitx5-unikey
```
```bash
sudo nano ~/.xprofile

export INPUT_METHOD=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```
- [fcitx shortcut](https://askubuntu.com/questions/736638/fcitx-wont-trigger-ime-on-superspace)

# iBus
```bash
GUI (or use pamac install --no-confirm)

ibus ibus-pinyin ibus-unikey ibus-bamboo

Edit ibus-bamboo PKGBUILD pkgver=0.6.7 sha256sums=('SKIP')
```
```bash
sudo nano ~/.xprofile

export INPUT_METHOD=ibus
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
```
```bash
sudo nano /usr/share/applications/ibus-daemon.desktop

[Desktop Entry]
Name=IBus Daemon
Exec=ibus-daemon -drx --panel=/usr/lib/kimpanel-ibus-panel
```

# KeepassXC
```bash
GUI (or use pamac install --no-confirm)

keepassxc

create database ~/Passwords with key ~/Passwords
```
```bash
nano ~/.xprofile

export PATH="$PATH:/home/ductran/bin"
```
```bash
copy /mnt/disk2/Projects/linux-config/files/applications/ to ~/.local/share/applications/
copy /mnt/disk2/Projects/linux-config/files/bin/ to ~/bin/
```
```bash
Add keepassxc-startup, keepassxc-watch to autostart scripts
```
- [Automatically unlock KeepassXC on startup and after lock screen](https://grabski.me/tech,/linux/2020/09/02/automatically-unlock-keepassxc-on-startup-and-after-lock-screen/)

# Config file dialog
```bash
GUI (or use pamac install --no-confirm)

xdg-desktop-portal
xdg-desktop-portal-kde
```
```bash
nano ~/.xprofile

export GTK_USE_PORTAL=1
```

# CPU Power
```bash
echo conservative | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```

# Tweaks
*  Unpin all app in task bar
*  Configure desktop --> Tweak --> Show the desktop toolbox: off
*  Configure appplication laucher --> Show application by name: on
*  Pin favorite apps: System Settings, Add or Remove Software, Dolphin, Vivaldi, Chrome, Firefox, Skype, Visual Studio Code, Webstorm, Rider, GitKraken
*  Configure Panel --> Screen Edge: Left
*  Edit panel --> Add widget --> Download new widget: Win7 volume mixer
*  Configure System Tray --> Extra items: clipboard, Device notifier, Display Configuration, KDE Connect, Media Player, Notification, Printer, Weather report
*  Configure System Tray --> Entries --> Hidden all
*  Configure System Tray --> Entries --> Auto: Notification, psensor, Clipboard
*  Edit panel --> Adnetd widget: Battery, Volume mixer, Network, Bluetooth, Touchpad, Input Method panel
*  Input Method panel --> Hide: fcitx, virtual keyboard, Telex, Unicode, Half width, Spell check, Macro, Full width input, No remind
*  Edit panel --> More Setting --> Auto hide
*  Lock widget

# Fix menu height
```bash
sudo nano /usr/share/plasma/plasmoids/org.kde.plasma.kickoff/contents/ui/FullRepresentation.qml

Layout.minimumHeight: PlasmaCore.Units.gridUnit * 45
```

# Theme (dark)
*  Global theme: Nordian Solid Global
*  Plasma style: Nordian Solid Plasma
*  Application Style: kvantum
*  GTK Theme: Nordian Breeze GTK
*  Window Decorators: Nordian Solid Aurorae
*  Color: kvantum
*  Icon: Breeze Nordian Dark Icon
*  SDDM: Nordian SDDM
*  Splash Screen: Nordian Solid Global
*  Kvantum: Nordian Kvantum
*  Wallpaper: Plasma Desktop Wallpaper 1591
*  Lock screen: Nordian-Plasma
*  Fix SDDM date Format
```bash
sudo nano /usr/share/sddm/themes/Nordian-SDDM/components/Clock.qml

"'The day is' dddd dd MMMM yyyy"
```

# Theme 2 (dark)
*  Global theme: Arc KDE
*  GTK Theme: Plane GTK Arc Dark
*  Icon: papirus dark
*  SDDM: KDE-Story
*  Application Style: kvantum
*  Kvantum: Arc Dark

# Theme 3 (light)
*  Install
```bash
GUI (or use pamac install --no-confirm)

breeze-gtk
lightly-qt
```
*  Global theme: Breeze
*  Plasma style: Breeze Light
*  Application Style: Lightly
*  GTK Theme: Breeze
*  Window Decorators: Lightly
*  Color: Breeze Light
*  Icon: Breeze
*  SDDM: Breeze
*  Splash Screen: Breeze
*  Wallpaper: Kite

# Theme 4 (light)
*  Install
```bash
GUI (or use pamac install --no-confirm)

aritim-light-kde
aritim-light-gtk
papirus-icon-theme
lightly-qt
```
*  Global theme: aritim-light
*  Plasma style: aritim-light
*  Application Style: Lightly
*  GTK Theme: aritim-light
*  Window Decorators: aritim-light
*  Color: aritim-light
*  Icon: Papirus light
*  SDDM: Breeze
*  Splash Screen: Breeze
*  Wallpaper: Kite

# Theme 5 (dark)
*  Install
```bash
GUI (or use pamac install --no-confirm)

aritim-dark-kde
aritim-dark-gtk
papirus-icon-theme
lightly-qt

sudo nano /usr/share/color-schemes/AritimDark.colors
[WM]
activeBackground=20,26,33,255
inactiveForeground=102,106,115,255

extract /mnt/disk2/Projects/linux-config/files/assets.zip to ~/.config/gtk-3.0/
copy /mnt/disk2/Projects/linux-config/files/share/ to /usr/share/
```
*  Global theme: aritim-dark
*  Plasma style: aritim-dark
*  Application Style: Lightly
*  GTK Theme: aritim-dark
*  Window Decorators: aritim-dark
*  Color: aritim-dark
*  Icon: Papirus dark
*  SDDM: Breeze
*  Splash Screen: Breeze
*  Wallpaper: Kite

# Plasmoid
*  Analog clock
*  System Monitor
*  hard disk activity
*  Network speed

# Chinese Font
```bash
sudo pacman -S noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
sudo pacman -S noto-fonts-sc noto-fonts-tc
sudo pacman -S ttf-roboto ttf-dejavu ttf-droid ttf-inconsolata ttf-indic-otf ttf-liberation
sudo pacman -S terminus-font
sudo pacman -S adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts
sudo pacman -S adobe-source-han-sans-tw-fonts adobe-source-han-serif-tw-fonts
sudo pacman -S wqy-microhei wqy-zenhei wqy-bitmapfont
sudo pacman -S opendesktop-fonts
```
*  optional: typographic font
```bash
sudo pacman -S ttf-arphic-ukai ttf-arphic-uming
```

# Windows Font
```bash
sudo cp /mnt/disk1/Windows/Fonts/* ~/.local/share/fonts
sudo fc-cache --force
```
- [Microsoft fonts](https://wiki.archlinux.org/index.php/Microsoft_fonts)

# GRUB Theme
```bash
yay -S grub2-theme-archxion
sudo nano /etc/default/grub

Replace #GRUB_THEME="/path/to/gfxtheme" by GRUB_THEME="/boot/grub/themes/Archxion/theme.txt"

grub-mkconfig -o /boot/grub/grub.cfg
```
- [Generator/Grub2-themes](https://github.com/Generator/Grub2-themes)

# Tips & Tricks
*  Pacman remove unused packages
```bash
sudo pacman -Rs $(pacman -Qdtq)
```
*  Clear cache files
```bash
sudo rm -rfv /tmp/*
sudo rm -rfv ~/.cache/*
```
