# Installation
 - [mjnadeli's guide](https://gist.github.com/mjnaderi/28264ce68f87f52f2cabb823a503e673)


# Wireless Configuration

## Enable `iwd`
 - `# systemctl enable iwd`
 - `# systemctl start iwd`

## Generate PreSharedKey
 - `# wpa_passphrase "my_ssid" "my_password"`

## Store network configuration
 - `/var/lib/iwd/my_ssid.psk`:
```
[Security]
PreSharedKey=aafb192ce2da24d8c7805c956136f45dd612103f086034c402ed266355297295

[Settings]
Autoconnect=true
```

## Configure `iwd` auto scan
 - `/etc/iwd/main.conf`:
```
[Scan]
disable_periodic_scan=false
```


# Network Configuration

## Enable `systemd-networkd`
 - `# systemctl enable systemd-networkd`
 - `# systemctl start systemd-networkd`
 - `/etc/systemd/network/25-wireless.network`:
```
[Match]
Name=wls128

[Network]
DHCP=ipv4
```

## Enable `systemd-resolved`
 - `# systemctl enable systemd-resolved`
 - `# systemctl start systemd-resolved`
 - `# ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf`


# Time Configuration

## Configure `systemd-timesyncd`
 - `# systemctl enable systemd-timesyncd`
 - `# systemctl start systemd-timesyncd`
 - `/etc/systemd/timesyncd.conf`:
```
[Time]
NTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
FallbackNTP=0.pool.ntp.org 1.pool.ntp.org 0.fr.pool.ntp.org
```


# Arch Linux Mirrorlist
 - `# curl "https://www.archlinux.org/mirrorlist/?country=US&protocol=https&ip_version=4&use_mirror_status=on" -o /etc/pacman.d/mirrorlist`


# Configure `vconsole`
 - `/etc/vconsole.conf`
```
KEYMAP=us
FONT=default8x16
```
 - `# systemctl restart systemd-vconsole-setup.service`


# sd-encrypt hook

[missing aic94xx wd719x](https://gist.github.com/imrvelj/c65cd5ca7f5505a65e59204f5a3f7a6d)


# sshd
 - `# systemctl enable sshd`
 - `# systemctl start sshd`


# X and i3wm

## Disable Intel Integrated Graphics Controller
 - `/etc/modprobe.d/blacklist.conf`:
```
install i915 /bin/false
```

## ATI HD 5750 driver
 - `# pacman -Sy mesa xf86-video-ati mesa-vdpau`

## Early KVM start
 - `/etc/mkinitcpio.conf`
```
MODULES=(... radeon ...)
```
 - `# mkinitcpio -p linux`

## X.org
 - `# pacman -Sy xorg-server xorg-apps xorg-xinit i3 numlockx`

## Display Manager
 - `# pacman -Sy lightdm lightdm-gtk-greeter`
 - `# pacman -Sy xdm-archlinux`
 - Make sure ``/.xinitrc` has execution permission, otherwise `xdm` cannot launch session.

## Fonts
 - `# pacman -Sy noto-fonts ttf-dejavu ttf-liberation ttf-inconsolata terminus-font ttf-font-awesome`

## i3 productivity tools
 - `# pacman -Sy pacman -S rxvt-unicode ranger rofi conky dmenu urxvt-perls perl-anyevent-i3 perl-json-xs`

## Additional tools for shell and ranger
 - `# pacman -Sy atool highlight elinks mediainfo w3m ffmpegthumbnailer mupdf`

## X Window apps
 - `# pacman -Sy chromium firefox vlc`

## Sound driver and tools
 - [https://wiki.archlinux.org/index.php/Advanced_Linux_Sound_Architecture#Installation](Arch Linux Wiki)
 - `# pacman -Sy alsa-utils alsa-plugins alsa-lib pavucontrol`
 - `$ aplay -l`
 - `$ lspci | grep -i audio`
 - `$ ls -l /dev/snd`
 - `$ alsamixer -c 1`
 - `$ amixer scontrols`
 - `amixer -c 1 cset name='IEC958 Playback Switch' on`
 - `$ speaker-test -c 1 -D hw:1,1`
 - `~/.asoundrc`
```
pcm.!default {
    type hw
    card MID
}

ctl.!default {
    type hw
    card MID
}
```
- Also, Firefox needs pulseaudio.  Refer to Arch Wiki to install and configure.


## Chinese configurations
 -  `# pacman -S fcitx fcitx-configtool fcitx-chewing`
 - `~/.Xresources`
```
URxvt.inputMethod: fcitx
```
 - `~/.bashrc`
```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
export LC_CTYPE=en_US.UTF-8
```
 - `~/.config/i3/config`
```
exec --no-startup-id fcitx -d
```

# Customization

## Pacman
 - `/etc/pacman.conf`: Uncomment `Color`

## Firefox
 - `about:config`: `layers.acceleration.force-enabled` set to true to prevent tearing when scroll pages.

