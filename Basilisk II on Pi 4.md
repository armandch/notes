# References
- [Mini PowerMac](https://hackaday.io/project/7867/instructions)
- [install Basilisk II without X11 on raspberry pi](https://gist.github.com/yangxuan8282/f1c8c19cc92a69d6f170ed03191ca1f1)

# Install Required Dependencies
- `sudo apt-get install git autoconf automake make gcc g++ libsdl1.2-dev libgtk2.0-dev libxxf86dga-dev libxxf86vm-dev libesd0-dev`

# Install Basilisk II
- `git clone https://github.com/cebix/macemu`
- `cd macemu/BasiliskII/src/Unix`
- `aclocal`
- `autoconf`
- `autoreconf -I ./m4`
- `./configure --enable-sdl-video --enable-sdl-audio --disable-vosf --disable-jit-compiler --without-gtk`
- `make install`

# Configure .basilisk_ii_prefs
```
cpu 4
modelid 14
ignoresegv true

rom /mnt/dietpi_userdata/Macintosh/QUADRA650.ROM
disk /mnt/dietpi_userdata/Macintosh/System761.dsk

screen win/640/480/16
```

# Configure DietPi to display 512x384 Fullscreen
- Edit `/boot/config.txt`:
```
framebuffer_width=512
framebuffer_height=384
hdmi_group=1
hdmi_mode=1
```
- Edit `.basilisk_ii_prefs`:
```
screen win/512/384/8
```

# Run Basilisk II in Framebuffer mode
- Configure using `--enable-fbdev-dga` instead of `--enable-sdl-video`
- Edit `.basilisk_ii_prefs`:
```
screen win/512/384/8
fbdevicefile /usr/local/share/BasiliskII/fbdevices
```
