# fedora_postinstall

### Theme
```
sudo dnf install adw-gtk3-theme papirus-icon-theme gnome-tweaks
flatpak install org.gtk.Gtk3theme.adw-gtk3 org.gtk.Gtk3theme.adw-gtk3-dark
sudo dnf copr enable peterwu/rendezvous
sudo dnf install bibata-cursor-themes
```

### Xpadneo
```
sudo dnf copr enable sentry/xpadneo
sudo dnf install xpadneo
```
### Steam flatpak
```
sudo dnf install steam-devices
```

### Nvidia
```
sudo nano /etc/environment
__GL_SYNC_DISPLAY_DEVICE=DP-2
```
### Fix boot logo
```
sudo nano /etc/plymouth/plymouthd.conf

# Administrator customizations go in this file
[Daemon]
#Theme=fade-in
DeviceScale=1

sudo dracut -f
```

### Open RGB
```
sudo dnf install openrgb-udev-rules
Exec=/usr/bin/flatpak run --branch=stable --arch=x86_64 --command=openrgb org.openrgb.OpenRGB --startminimized --profile "fedora"
```

### Repo RPM Fusion
```
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf group update core
```

### Alias
```
sudo nano ~/.bashrc
alias update-grub='sudo grub2-mkconfig -o /boot/grub2/grub.cfg'
```

### Flatpak
```
flatpak install com.bitwarden.desktop com.discordapp.Discord com.github.tchx84.Flatseal com.heroicgameslauncher.hgl com.mattjakeman.ExtensionManager com.spotify.Client com.valvesoftware.Steam com.visualstudio.code de.haeckerfelix.Fragments io.freetubeapp.FreeTube io.github.giantpinkrobots.flatsweep io.gitlab.news_flash.NewsFlash net.cozic.joplin_desktop net.lutris.Lutris org.onlyoffice.desktopeditors org.openrgb.OpenRGB org.raspberrypi.rpi-imager org.ryujinx.Ryujinx org.signal.Signal com.github.IsmaelMartinez.teams_for_linux org.videolan.VLC org.mozilla.firefox org.gnome.meld org.gnome.Rhythmbox3 org.gnome.Evolution org.gimp.GIMP org.chromium.Chromium com.protonvpn.www ch.protonmail.protonmail-bridge

flatpak update
```
### Bridges IPs Gnome boxes
```
sudo systemctl enable virtnetworkd.service
```
### Secure Boot
```
sudo kmodgenca -a
sudo mokutil --import /etc/pki/akmods/certs/public_key.der
sudo akmods --force
sudo dracut --force
```
