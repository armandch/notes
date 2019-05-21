# SSD Optimization
1. Should do ext4 Journaling. Make sure has_journaling is present by checking file system features using either of the following commands:
    sudo dumpe2fs /dev/sda1 | more
    debugfs -R features /dev/sda1
2. Should disable excessive file metadata for ext4 by using `noatime` (`noatime` automatically enables `nodiratime`). Make sure in /etc/fstab `noatime` is there for all ext4 partitions.
3. Update firmware. [Reference](https://wiki.debian.org/SSDOptimization#Upgrading_the_Firmware)
4. For TRIM, choose to do thin-provisioning instead of over-provisioning. Reference [this](https://wiki.debian.org/SSDOptimization#Mounting_SSD_filesystems) and [this](http://blog.neutrino.es/2013/howto-properly-activate-trim-for-your-ssd-on-linux-fstrim-lvm-and-dmcrypt/).
5. Limit swap wear:
    # /etc/sysctl.d/local.conf
    vm.swappiness=1
6. Low latency IO-Scheduler. [Reference](https://wiki.debian.org/SSDOptimization#Low-Latency_IO-Scheduler)
7. Choose to use suspension/hibernate.
8. Choose not to disable Chrome caching.

# Wifi
1. Find your wireless interface and bring it up:
    ip a
    iwconfig
    ip link set wlan0 up
2. Scan for available networks and get network details:
    iwlist scan
3. For WPA-PSK and WPA2-PSK, first change config file permission:
    chmod 0600 /etc/network/interfaces
4. Then generate correct WPA PSK hash for your SSID:
    wpa_passphrase myssid my_very_secret_passphrase
5. Then edit `/etc/network/interfaces`:
    auto wlan0
    iface wlan0 inet dhcp
            wpa-ssid myssid
            wpa-psk myhash
4. Bring your interface up:
    ifup wlan0

# Configure apt-get --no-install-recommends
    cat > /etc/apt/apt.conf.d/01norecommend << EOF
    APT::Install-Recommends "0";
    APT::Install-Suggests "0";
    EOF

# Install AMD/ATI Proprietary Driver (Jessie)
1. Instructions [here](https://wiki.debian.org/ATIProprietary).
2. aptitude update
3. aptitude -r install linux-headers-$(uname -r|sed 's,[^-]*-[^-]*-,,') fglrx-driver
4. aticonfig --initial

# Install AMD/ATI Proprietary Driver (Jessie, Stretch)
1. Install OSS ATI driver.
2. Install non-free firmware.

# Install Google Chrome Browser Using PPA
1. wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
2. sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
3. sudo apt-get update
4. sudo apt-get install google-chrome-stable
5. Create alias for 'google-chrome-stable --disk-cache-size=1 --media-cache-size=1'

# Enhance CJK Fonts for Google Chrome
1. Download Noto Sans CJK JP, KR, SC, TC from [here](https://www.google.com/get/noto/).
2. Install fonts by referencing [here](https://www.google.com/get/noto/help/install/).
3. Install Advanced Font Settings extension for Chrome.
4. Change fonts for scripts: Han, Hangul, Japanese, and Traditional Han.

# Install Chinese Input Method
1. sudo apt-get install ibus ibus-chewing im-config
2. sudo apt-get install fonts-arphic-ukai fonts-arphic-uming fonts-ipafont-mincho fonts-ipafont-gothic fonts-unfonts-core
3. ibus-setup
4. Add Chewing into input method list.
5. sudo im-config -n ibus
6. Re-login
7. Go to Settings > Region & Language, add Chinese (Chewing) as input sources.

# Install Dropbox (Manual)
1. Referencing [here](https://www.dropbox.com/en/help/246).
2. Install [Dropbox](https://www.dropbox.com/install-linux).
3. Install dropbox.py to control Dropbox.
4. Create dropbox.desktop under ~/.config/autostart:
    Name=Dropbox
    GenericName=File Synchronizer
    Comment=Sync your files across computers and to the web
    Exec=/home/armandch/bin/dropbox.py start
    Terminal=false
    Type=Application
    Icon=dropbox
    Categories=Network;FileTransfer;
    X-GNOME-Autostart-enabled=true
    StartupNotify=true

#Install Dropbox (Gnome 3)
1. sudo aptitude install nautilus-dropbox

# Enable exfat
1. sudo apt-get install exfat-fuse exfat-utils

# Partition and Format USB
1. sudo dd if=/dev/zero of=/dev/sda bs=512 count=1
2. sudo fdisk /dev/sda
3. Create DOS partition table.
4. Create partitions.
5. Set bootable partition.
6. Change filesystem type of partitions.
7. Write and quit.
8. sudo mkfs.vfat /dev/sda1
9. sudo fatlabel /dev/sda1 KINGSTON_1G

# Show whether Wayland or X11 is being used
1. loginctl
2. loginctl show-session <YOUR_NUMBER> -p Type

# Nestopia and Fceux sound crackling
1. Add `export PULSE_LATENCY_MSEC=30` to `~/.bashrc`.
2. Add `export PULSE_LATENCY_MSEC=30` to `~/.gnomerc`.

# Wine sound problem
1. Run `winetricks --gui` and set `sound=alsa`.

# Wine create prefix
1. Let Wine create path.
2. `env WINEPREFIX=$prefix WINEARCH=win32/win64 winecfg`

# Ultima Online in Wine
1. Run `env WINEPREFIX=$prefix WINEARCH=win32 winecfg` to create prefix.
2. Install dotnet20 through winetricks: `env WINEPREFIX=$prefix winetricks --gui`.
3. Install wine_gecko: `env WINEPREFIX=$prefix wine msiexec /i wine_gecko-2.47-x86.msi`.
4. Install d3dx9_36 through winetricks.
4. winetricks: `ddr=gdi glsl=enabled multisampling=enabled psm=enabled rtlm=auto sound=alsa strictdrawordering=disabled windowmanagerdecorated=n windowmanagermanaged=n`

# Remove i386 Architecture
1. sudo dpkg --get-selections | grep i386 | awk '{print $1}'
2. sudo apt-get remove --purge `dpkg --get-selections | grep i386 | awk '{print $1}'`
3. sudo dpkg --remove-architecture i386
4. sudo apt-get update

# GOG games no sound
1. Rename `<GAME>/game/lib64` to something else.

# Needrestart
1. [ToDo](https://www.debian.org/releases/stable/amd64/release-notes/ch-whats-new.en.html#security)


# MAME
1. mame apple2ee -flop1 ~/mame/games/disk.dsk -effect rgb3_kb


# Toshiba R935
1. After finishing installation, enter recovery mode and force grub-efi installation to the removable media path to work around buggy Toshiba UEFI firmware.
