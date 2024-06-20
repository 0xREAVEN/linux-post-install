# 🚀 Memo Post-Installation Arch Linux

Ne pas installer les drivers NVIDIA avec Archinstall

#### 1. Optimiser pacman

```
sudo nano /etc/pacman.conf
```

Décommentez (retirez le **#** des lignes suivantes) :
   
```
#Options diverses
#UseSyslog
Color <-
#NoProgressBar
#CheckSpace
VerbosePkgLists <- 
ParallelDownloads = 5 <-
ILoveCandy <-
```

#### 2. **Installation de Yay**
  
```
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg -si
```

#### 3. Compilation multithread des paquets AUR :

```
sudo nano /etc/makepkg.conf
```

Pour utiliser tous les threads, ajoutez :

```
MAKEFLAGS="-j$(nproc)"
```

## SUPPORT MATÉRIEL

#### 1. Installer les composants de base :

```
sudo pacman -S --needed nvidia-dkms nvidia-utils lib32-nvidia-utils nvidia-settings vulkan-icd-loader lib32-vulkan-icd-loader
```

#### 2. Activer nvidia-drm.modeset=1 :

```
sudo nano /etc/modprobe.d/nvidia.conf
```

Ajouter:

`options nvidia-drm modeset=1`

Sauvegarder.
   
#### Imprimantes Canon
- Pilotes Imprimante

```
yay -S foomatic-db-engine foomatic-db foomatic-db-ppds foomatic-db-nonfree foomatic-db-nonfree-ppds gutenprint foomatic-db-gutenprint-ppds cups-bjnp
sudo systemctl enable --now avahi-daemon cups
```

- Scanner

```
yay -S sane sane-airscan skanlite
```

#### Bluetooth

```
yay -S --needed bluez bluez-utils bluez-plugins
sudo systemctl enable --now  bluetooth.service
```

## LOGICIEL DE BASE

#### Composants de base

```
yay -S --needed gst-plugins-bad gst-plugins-base gst-plugins-ugly gst-plugin-pipewire gstreamer-vaapi gst-plugins-good gst-libav gstreamer downgrade rebuild-detector xdg-desktop-portal-gtk xdg-desktop-portal neofetch power-profiles-daemon lib32-pipewire hunspell hunspell-fr p7zip unrar ttf-liberation noto-fonts noto-fonts-emoji adobe-source-code-pro-fonts otf-font-awesome ttf-droid ntfs-3g fuse2fs exfat-utils fuse2 fuse3 bash-completion man-db man-pages dosfstools
```

#### Logiciels KDE

```
sudo pacman -S --needed xdg-desktop-portal-kde okular print-manager gwenview spectacle partitionmanager ffmpegthumbs qt6-wayland kdeplasma-addons powerdevil kcalc plasma-systemmonitor qt6-multimedia qt6-multimedia-gstreamer qt6-multimedia-ffmpeg kwalletmanager ktorrent kdeconnect kaccounts-providers
```


#### Autres logiciels
```
yay -S freetube-bin virtualbox virtualbox-guest-iso virtualbox-host-dkms vde2 ryujinx-bin joplin-appimage translate-shell rpi-imager ledger-live-bin firefox thunderbird thunderbird-i18n-fr arch-update onlyoffice-bin vlc discord gimp visual-studio-code-bin spotify bitwarden chromium signal-desktop etcher-bin
```

#### Thunderbird extension

https://addons.thunderbird.net/fr/thunderbird/addon/tbsync/?src=cb-dl-users

https://addons.thunderbird.net/fr/thunderbird/addon/dav-4-tbsync/

#### Pare-feu

```
sudo pacman -S --needed --noconfirm firewalld python-pyqt5 python-capng
sudo systemctl enable --now firewalld.service
firewall-applet &
```

#### Reflector pour la mise à jour automatique des miroirs

```
yay -S reflector-simple
```

```
sudo reflector --verbose --score 100 --latest 20 --fastest 5 --sort rate --save /etc/pacman.d/mirrorlist
```
#### Octopi

```
yay -S octopi octopi-notifier-qt5
```

#### Timeshift

```
sudo pacman -S timeshift
```

```
sudo systemctl enable --now cronie
```
  
#### Fish
    
```
sudo pacman -S fish                     # 1. installez fish
chsh -s /usr/bin/fish                   # 2. Définissez-le par défaut.
fish                                    # 3. Lancez fish ou redémarrez et il sera par défaut.
fish_update_completions                 # 4. Mettez à jour les complétions.
set -U fish_greeting                    # 5. Supprimez le message de bienvenue.
sudo nano ~/.config/fish/config.fish    # 6. Créez un alias comme pour bash au début de ce tutoriel.
```
- Ajoutez ensuite les alias suivants entre if et end :

```
    alias arch-update-mirrors='sudo reflector --verbose --score 100 --latest 20 --fastest 5 --sort rate --save /etc/pacman.d/mirrorlist'
    alias arch-fix-key='sudo rm /var/lib/pacman/sync/* && sudo rm -rf /etc/pacman.d/gnupg/* && sudo pacman-key --init && sudo pacman-key --populate && sudo pacman -Sy --noconfirm archlinux-keyring && sudo pacman --noconfirm -Su'
    alias arch-errors='journalctl -p 3 -xb'
    alias dolphin-root='pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY KDE_SESSION_VERSION=5 KDE_FULL_SESSION=true dolphin'
```
Changer la couleur de l'utilsateur
```
sudo nano ~/.config/fish/config.fish
```
Ajouter :
```
set -U fish_color_user blue
```
Tide :

```
sudo pacman -S fisher ttf-meslo-nerd-font-powerlevel10k
fisher install IlanCosman/tide@v6
tide configure
```

#### OpenRGB
```
yay -S openrgb-bin
```

#### Personnalisation

```
yay -S papirus-icon-theme arc-kde-git arc-gtk-theme
```
Ouvrir Configuration du système, Apparence, Style d'applications, Configurer un style pour applications "GNOME/GTK", thème GTK : Arc-Dark

Application du thème sur Timeshift ou GParted :
```
sudo cp -r ~/.config/gtk-3.0 /root/.config/
```
```
sudo cp -r ~/.config/gtk-4.0 /root/.config/
```

config.conf au dessus pour neofetch

Systemd boot
```
sudo nano /boot/loader/loader.conf
```
```
timeout 8
console-mode max
```

## Gaming

### Steam

```
sudo pacman -S steam
```
Start Minimized
```
nano ~/.config/autostart/steam.desktop
Exec=/usr/bin/steam-runtime %U -silent
```

### Lutris

```
sudo pacman -S lutris wine-staging
```
### Heroic
```

yay -S heroic-games-launcher-bin
```

### Support manette Xbox

```
yay -S xpadneo-dkms
```

### Affichage des performances en jeu

```
sudo pacman -S goverlay
```

### vm max count


```
sudo nano /etc/sysctl.d/99-sysctl.conf
```

```
vm.max_map_count=2147483642
```
### Script kwin
Ajouter le script kwin "Autocomposer".

## Tips

### Discord

```
nano ~/.config/discord/settings.json
```

```
{
  "SKIP_HOST_UPDATE": true,
  "IS_MAXIMIZED": true,
  "IS_MINIMIZED": false,
  "MINIMIZE_TO_TRAY": true,
  "OPEN_ON_STARTUP": false,
  "WINDOW_BOUNDS": {
    "x": 0,
    "y": 30,
    "width": 1920,
    "height": 1013
  }
}
```

### Erreur sur mon PC

event2: Failed to call EVIOCSKEYCODE with scan code 0xc01cb, and key code 108: Invalid argument
```
sudo nano /etc/modprobe.d/EVIOCSKEYCODE.conf
```
```
blacklist eeepc_wmi
```

### 144Hz

```
sudo nano ~/.config/plasma-workspace/env/path.sh
```

```
export KWIN_X11_NO_SYNC_TO_VBLANK=1
export KWIN_X11_REFRESH_RATE=144000
export KWIN_X11_FORCE_SOFTWARE_VSYNC=1
```
Dans les paramètres OpenGL, désactivez les options suivantes :

"Allow Flipping"

Assurez-vous de cocher les options "Force Composition Pipeline" et "Force Full Composition Pipeline" pour éviter les déchirures d'écran.

Une fois la configuration terminée, cliquez sur "Save to X Configuration File" pour enregistrer les paramètres.

Enfin, ajoutez la commande suivante au démarrage de votre système :

```
nvidia-settings --load-config-only
```

### FSTAB
```
sudo nano /etc/fstab
```
```
#Mes disques durs
/dev/sda1    /mnt/data     ext4    defaults,auto,noatime 0 2
/dev/sdb1    /mnt/games    ext4    defaults,auto,noatime 0 2
/dev/sdc1    /mnt/backup   ext4    defaults,auto,noatime 0 2
```
