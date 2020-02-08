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

# Firefox
```bash
https://download.mozilla.org/?product=firefox-latest&os=linux64&lang=vi
sudo tar xjf firefox-*.tar.bz2 -C /opt/
sudo ln -s /opt/firefox/firefox /usr/bin/firefox
sudo cp /opt/firefox/browser/chrome/icons/default/default128.png /usr/share/icons/hicolor/128x128/apps/firefox.png
sudo nano cd /usr/share/applications/firefox.desktop

[Desktop Entry]
Version=1.0
Name=Mozilla Firefox
# Only KDE 4 seems to use GenericName, so we reuse the KDE strings.
# From Ubuntu's language-pack-kde-XX-base packages, version 9.04-20090413.
GenericName=Web Browser
# Gnome and KDE 3 uses Comment.
Comment=Access the Internet
Exec=/opt/firefox/firefox

StartupNotify=true
Terminal=false
Icon=firefox
Type=Application
Categories=Network;WebBrowser;
MimeType=text/html;text/xml;application/xhtml_xml;image/webp;x-scheme-handler/http;x-scheme-handler/https;x-scheme-handler/ftp;
Actions=new-window;new-private-window;

[Desktop Action new-window]
Name=New Window
Exec=/opt/firefox/firefox

[Desktop Action new-private-window]
Name=New Incognito Window
Exec=/opt/firefox/firefox -private-window

```