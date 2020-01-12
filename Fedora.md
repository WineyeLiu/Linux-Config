# My Fedora KDE installation

# Setting
*  Global theme: Breeze Dark
*  Plasma style: Breeze Dark
*  Workspace Behavior --> General behavior: Double click
*  Workspace Behavior --> Screen locking: Off
*  Workspace Behavior --> Screen edge: Off
*  Shortcut --> Global shortcut --> KRunner --> Global alternative: Meta + Space
*  Shortcut --> Global shortcut --> KRunner --> Global alternative: Clear
*  Regional Setting --> Language: English
*  Regional Setting --> Language: English
*  Regional Setting --> Format: Vietnamese
*  Regional Setting --> Format --> Number: Default
*  Regional Setting --> Format --> Currency: Default
*  Input Devices --> Mouse --> Pointer speed: 4, flat
*  Input Devices --> Touch pad --> Tap to click: On
*  Display and Monitor --> Compositor --> Animation speed: Instant
*  Display and Monitor --> Compositor --> Render backend: OpenGL 3.1
*  Power Management --> AC Power --> Brightness: 100%
*  Power Management --> AC Power --> Dim screen: 30
*  Power Management --> AC Power --> Screen energy saving: 35
*  Power Management --> AC Power --> Suspend session: Off
*  Power Management --> AC Power --> Lid close: Turn off screen
*  Power Management --> AC Power --> Wireless: On
*  Power Management --> Battery --> Brightness: 100%
*  Power Management --> Battery --> Dim screen: 30
*  Power Management --> Battery --> Screen energy saving: 35
*  Power Management --> Battery --> Suspend session: Off
*  Power Management --> Battery --> Lid close: Turn off screen
*  Power Management --> Battery --> Wireless: On
*  Power Management --> Low Battery --> Brightness: 40%
*  Power Management --> Low Battery --> Dim screen: 5
*  Power Management --> Low Battery --> Screen energy saving: 10
*  Power Management --> Low Battery --> Suspend session: 15
*  Power Management --> Low Battery --> Lid close: Sleep
*  Power Management --> Advanced Setting --> Critical level: Shut down
*  Removeable Storage --> Removeable Devices --> Enable automatic mouting: On

# Full system update
```bash
sudo dnf update --refresh
```

# Add RPM Fusion repositories
```bash
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf groupupdate core
```

# NVIDIA drivers
```bash
sudo dnf install fedora-workstation-repositories
sudo dnf config-manager rpmfusion-nonfree-nvidia-driver --set-enabled
sudo dnf install xorg-x11-drv-nvidia-390xx akmod-nvidia-390xx
sudo dnf install acpi
sudo dnf copr enable chenxiaolong/bumblebee
sudo dnf install akmod-bbswitch bumblebee primus
sudo gpasswd -a $USER bumblebee
sudo systemctl enable bumblebeed
sudo systemctl mask nvidia-fallback

sudo dnf install intel-gpu-tools
```

- [NVIDIA Optimus Bumblebee](https://docs.fedoraproject.org/en-US/quick-docs/bumblebee/)

# Google Chrome
```bash
sudo dnf config-manager --set-enabled google-chrome
sudo dnf install google-chrome-stable
```

# Vivaldi
```bash
sudo dnf config-manager --add-repo https://repo.vivaldi.com/archive/vivaldi-fedora.repo
sudo dnf install vivaldi-stable
```

# Adobe Flash
```bash
sudo dnf install http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
sudo dnf install flash-plugin alsa-plugins-pulseaudio libcurl
```

# Skype
```bash
sudo curl -o /etc/yum.repos.d/skype-stable.repo https://repo.skype.com/rpm/stable/skype-stable.repo
sudo dnf install skypeforlinux
```

# IDE & Compiler
- [Fedora Developer Portal](https://developer.fedoraproject.org/)

# Java
```bash
sudo dnf install java-latest-openjdk.x86_64
```

# .NET Core
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -q -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/30/prod.repo
sudo dnf install dotnet-sdk-3.1
```
- [Install .NET Core Fedora](https://docs.microsoft.com/vi-vn/dotnet/core/install/linux-package-manager-fedora30)

# Nodejs
```bash
sudo curl -sL https://rpm.nodesource.com/setup_13.x | sudo bash -
sudo dnf install -y nodejs
sudo npm install -g @angular/cli
echo "fs.inotify.max_user_watches=524288" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```
- [NodeSource Node.js Binary Distributions](https://github.com/nodesource/distributions/blob/master/README.md#rpm)

# MariaDB
```bash
sudo systemctl start mariadb
mysql_secure_installation
```

# VS Code
```bash
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo dnf install code
```

# Jetbrains Toolbox
```bash
sudo tar xfz jetbrains-toolbox-*.tar.gz -C /usr/local/bin --strip-components 1
sudo chmod 777 /usr/local/bin/jetbrains-toolbox
```
*  Install Webstorm
*  Install IDEA
*  Install Rider
*  Install Datagrip
- [Download Jetbrains toolbox](https://www.jetbrains.com/toolbox-app/)

# Psensor
```bash
sudo dnf copr enable angeldm/psensor 
sudo dnf install psensor
```

# Yakuake
```bash
sudo dnf install yakuake
```

# Fcitx
```bash
sudo dnf install fcitx
sudo dnf install fcitx-qt4 fcitx-qt5
sudo dnf install fcitx-unikey
sudo dnf install kcm-fcitx
sudo nano ~/.config/fcitx/config
```
```bash
sudo nano /etc/profile.d/fcitx.sh
export XMODIFIERS="@im-fcitx"
export QT_IM_MODULE=fcitx
export GTK_IM_MODULE=fcitx
```
- [fcitx shortcut](https://askubuntu.com/questions/736638/fcitx-wont-trigger-ime-on-superspace)

# Automount partition
```bash
sudo mkdir /mnt/disk1
sudo mkdir /mnt/disk2
sudo mkdir /mnt/disk3
sudo blkid /dev/sda4
sudo blkid /dev/sdb1
sudo blkid /dev/sdb2
sudo nano /etc/fstab

UUID=01D5AFE0D7508090   /mnt/disk1  ntfs    defaults        0 0
UUID=01D5308C5EDFFD30   /mnt/disk2  ntfs    defaults        0 0
UUID=01D5308C6B0D0DF0   /mnt/disk3  ntfs    defaults        0 0
```

# Remove old kernel
```bash
sudo dnf remove kernel*5.3.7-301.fc31.x86_64
```