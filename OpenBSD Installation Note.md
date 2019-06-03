# Preparation

## References
- [Install OpenBSD on a Desktop](https://www.romanzolotarev.com/openbsd/install.html)
- [Installing OpenBSD 6.3 on your laptop is really hard (not)](https://sohcahtoa.org.uk/openbsd.html)
- [OpenBSD FAQ - Installation Guide](https://www.openbsd.org/faq/faq4.html#Partitioning)

## Create Installation USB Drive (on MacOS X)
1. `$ curl -O https://cloudflare.cdn.openbsd.org/pub/OpenBSD/6.3/amd64/SHA256`
2. `$ curl -O https://cloudflare.cdn.openbsd.org/pub/OpenBSD/6.3/amd64/install63.fs`
3. `$ grep install63.fs SHA256 | cut -f 4 -d ' '`
4. `$ shasum -a 256 install63.fs | cut -f 1 -d ' '`
5. Run `diskutil list` to find out identifier of the USB drive. It is `/dev/disk2` in my case.
6. `$ diskutil umount /dev/disk2s1`
7. `$ sudo dd if=install63.fs of=/dev/disk2 bs=1m`

## Create Firmwares Drive
1. Download all files from `http://firmware.openbsd.org/firmware/6.3/` and copy them to USB drive.

## Figure out USB Device Information
1. `$ doas fdisk sd1`
2. `$ doas disklabel sd1`
3. `$ doas mount /dev/sd1i /mnt/firmwares`

## Verify Firmwares (on OpenBSD)
1. Verify firmwares: `$ signify -C -p /etc/signify/openbsd-63-fw.pub -x /mnt/firmwares/SHA256.sig /mnt/firmwares/*.tgz`
2. Auto detect required firmware during installation: `fw_update -p /mnt/firmwares`.

## Special Things to Do for Toshiba Portege R935-ST4N01 Before Installation
1. Press F2 to enter bios setup.
2. Disable Secure Boot in bios.
3. Enable UEFI Boot in bios.
4. `boot> machine video 3`
5. `boot> boot`
6. After installation is done, edit `/etc/boot.conf`:
```
machine video 3
boot
```

## Special Things to Do for Thinkpad X1C6 Before Installation
1. Press ENTER to enter bios setup.
2. Disable Secure Boot in bios.
3. Enable UEFI Boot in bios: "Both".

# Installation

## Full Disk Encryption
1. Boot using USB installation drive.
2. Select (S)hell.
3. Erase all data on sd0. This will take very long time: `# dd if=/dev/urandom of=/dev/rsd0c bs=1m`
4. Create new GPT layout and EFI boot partition: `# fdisk -i -g -b 960 /dev/rsd0c`
5. Create software raid partition for the entire disk: `# disklabel -E sd0`. Options: `a a\n\n\nRAID\nw\nq\n`
6. Create encrypted software raid `# bioctl -c C -l sd0a softraid0`. Crypto volume will be attached as sd3
7. sd3 does not exist in `/dev` yet. Let's create it: `# cd /dev && sh MAVEDEV sd3`
8. To avoid problems, it is reasonable to clear the beginning of the installation drive. `# dd if=/dev/zero of=/dev/rsd3c bs=1m count=1`
9. `# exit`

## Install OpenBSD on sd3
1. Skip network configuration for now.
2. Timezone: America/New_York

# Post Installation

## Install firmware
1. `# mount /dev/sd1i /mnt/firmwares && fw-update -p /mnt/firmwares/`
2. `# shutdown -r now`

## Configure Wifi
1. `# vi /etc/hostname.iwn0`
    nwid my_nwid wpakey my_wpakey
    dhcp
2. `# chmod 640 /etc/hostname.iwn0`
3. `# /etc/netstart`

## syspatch
1. `# echo 'https://fastly.cdn.openbsd.org/pub/OpenBSD' > /etc/installurl`
2. `# syspatch`

## Openup
1. Install `openup` from [M:tier](https://stable.mtier.org/).

## softdep and noatime
1. `# sed -i 's/rw/rw,softdep,noatime/' /etc/fstab`

## Enable apmd
1. `# rcctl enable apmd`
2. `# rcctl set apmd flags -A -z 7`
3. `# rcctl start apmd`

## Configure doas
1. `# echo 'permit nopass username' > /etc/doas.conf`

## Add user to staff group
1. `# usermod -G staff username`

## X.org
1. Starting with OpenBSD 6.5, the Xorg binary is no longer installed setuid, so startx(1) can no longer be used by non-root users. The xenodm(1) display manager has to be used instead.
2. `# rcctl enable xenodm`
3. `# rcctl start xenodm`

## Troubleshooting: Relinking to create unique kernel failed
1. `# sha256 /bsd > /var/db/kernel.SHA256`

## Display CJK Characters
1. `# pkg_add noto_cjk`

## Configure tpm Plugin Manager for tmux
1. `# pkg_add bash`

## Install i3wm
1. `# pkg_add i3`

## Install Chinese Input Method
1. `# pkg_add fcitx-chewing`
2. In `.profile` add the following lines:
    LANG=en_US.UTF-8 
    LC_ALL=en_US.UTF-8 
    LC_CTYPE=en_US.UTF-8 
3. In `.xinitrc` add the following lines:
    export XMODIFIERS=`@im=fcitx`
    export GTK_IM_MODULE=fcitx
    export QT_IM_MODULE=fcitx
    /usr/local/bin/fcitx -d
4. (Work-around) Edit `~/.config/fcitx/profile` and make it read-only.

## i3wm config

  # Layout mode for new containers
  workspace_layout tabbed

  # Wallpaper
  exec feh --bg-scale ~/Pictures/Wallpapers/openbsd-wireframe-1366x768.png

  # Window effects
  exec --no-startup-id compton

  # Lock screen
  bindsym $mod+Control+l exec i3lock -i ~/Pictures/Wallpapers/wallpaper-1-1366x768.png

## i3status config

  general {
          output_format = "i3bar"
          colors = true
          interval = 5
  }
  
  order += "cpu_temperature cpu0"
  order += "cpu_temperature acpitz0"
  order += "wireless _first_"
  order += "volume master"
  order += "battery all"
  order += "tztime local"
  
  cpu_temperature cpu0 {
           format = "C: %degrees C"
           path = "cpu0"
  }
  
  cpu_temperature acpitz0 {
          format = "TZ: %degrees C"
  }
  
  wireless _first_ {
          format_up = "W: %quality at %essid"
          format_down = "W: down"
  }
  
  volume master {
          format = "vol: %volume"
  }
  
  battery all {
          format = "%status %percentage \% %remaining"
  }
  
  tztime local {
          format = "%a %b %d, %Y %I:%M %p"
  }

## Tools to use with i3wm
- ranger
- feh (or gpicview)
- zathura
- cmus
- smplayer
