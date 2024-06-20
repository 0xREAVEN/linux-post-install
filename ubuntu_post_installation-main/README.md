# ubuntu_post_installation

```
sudo apt autoremove --purge snapd
sudo apt-mark hold snapd
```

```
sudo apt install flatpak
sudo apt install gnome-software-plugin-flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

```
sudo apt install timeshift gnome-tweaks
```

```
sudo add-apt-repository ppa:papirus/papirus
sudo apt-get update
sudo apt-get install papirus-icon-theme
```
```
sudo cp 60-openrgb.rules /usr/lib/udev/rules.d/
sudo cp 20-hw1.rules /usr/lib/udev/rules.d
```
```
sudo apt-get install dkms linux-headers-`uname -r`
cd xpadneo
sudo ./install.sh
```
