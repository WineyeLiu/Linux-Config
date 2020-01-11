# My Fedora KDE installation


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
