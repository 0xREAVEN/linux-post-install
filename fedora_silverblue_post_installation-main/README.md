# fedora_silverblue_post_installation

```
sudo rpm-ostree install akmod-nvidia xorg-x11-drv-nvidia
sudo rpm-ostree kargs --append=rd.driver.blacklist=nouveau --append=modprobe.blacklist=nouveau --append=nvidia-drm.modeset=1 initcall_blacklist=simpledrm_platform_driver_init
```

```
sudo nano /etc/environment
__GL_SYNC_DISPLAY_DEVICE=DP-2
```

```
RPM Fusion :
rpm-ostree install \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

sudo reboot

 rpm-ostree update \
--uninstall $(rpm -q rpmfusion-free-release) \
--uninstall $(rpm -q rpmfusion-nonfree-release) \
--install rpmfusion-free-release \
--install rpmfusion-nonfree-release
```

```
sudo rpm-ostree override remove gnome-tour
```

```
sudo rpm-ostree install gnome-tweak-tool adw-gtk3-theme openrgb-udev-rules steam-devices
```

```
flatpak install org.gtk.Gtk3theme.adw-gtk3 org.gtk.Gtk3theme.adw-gtk3-dark com.bitwarden.desktop com.discordapp.Discord com.github.tchx84.Flatseal com.heroicgameslauncher.hgl com.mattjakeman.ExtensionManager com.spotify.Client com.valvesoftware.Steam com.visualstudio.code de.haeckerfelix.Fragments io.freetubeapp.FreeTube io.github.giantpinkrobots.flatsweep io.gitlab.news_flash.NewsFlash net.cozic.joplin_desktop net.lutris.Lutris org.onlyoffice.desktopeditors org.openrgb.OpenRGB org.raspberrypi.rpi-imager org.ryujinx.Ryujinx org.signal.Signal com.github.IsmaelMartinez.teams_for_linux org.videolan.VLC org.mozilla.firefox org.gnome.meld org.gnome.Rhythmbox3 org.gnome.Evolution org.gimp.GIMP org.chromium.Chromium com.protonvpn.www ch.protonmail.protonmail-bridge
```
```
```
echo "force_drivers+=\" nvidia nvidia_modeset nvidia_uvm nvidia_drm \"" | sudo tee /etc/dracut.conf.d/nvidia.conf > /dev/null
```
```
```
sudo rpm-ostree kargs --append=nvidia-drm.fbdev=1
```
