# My Fedora KDE installation

# Setting
*  Global theme: Breeze Dark
*  Plasma style: Breeze Dark
*  Workspace Behavior --> General behavior: Double click
*  Workspace Behavior --> Screen locking: Off
*  Workspace Behavior --> Screen edge: Off
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
```
- [NodeSource Node.js Binary Distributions](https://github.com/nodesource/distributions/blob/master/README.md#rpm)