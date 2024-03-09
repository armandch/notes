# Inform Notes

## Build Inform on macOS
git clone git@gitlab.com:DavidGriffith/frotz.git

### If building against specific tag
git ls-remote --tags
git checkout tags/6.34-6.12.2 -b 6.34-6.12.2

### Build
git submodule init
git submodule update
make submodules
make
sudo make install


## blorbtool
```
blorbtool.py -n my.gblorb import Exec 0 GLUL game.ulx
blorbtool.py my.gblorb import Pict 1 JPEG pict-0.jpg
blorbtool.py my.gblorb import Pict 2 JPEG pict-1.jpg
blorbtool.py my.gblorb import Pict 3 JPEG pict-2.jpg
blorbtool.py my.gblorb import Pict 4 JPEG pict-3.jpg
blorbtool.py my.gblorb import Snd 5 MOD music-0.mod
```

## IFM
sudo dnf install autoconf automake libtool flex byacc help2man
autoreconf -f -i -Wall,no-obsolete
./configure
make
sudo make install


## Build frotz on macOS
- Install MacPorts
- (Deprecated) sudo port install pkgconfig libao libsndfile libsamplerate freetype libpng libjpeg-turbo libsdl2 libsdl2_mixer
- brew install ncurses pkg-config sdl2 sdl2_mixer freetype jpeg zlib libao libsndfile libsamplerate libmodplug
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/ncurses/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/sdl2/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/sdl2_mixer/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/freetype/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/libjpeg/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/zlib/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/libao/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/libsndfile/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/libsamplerate/lib/pkgconfig
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/opt/libmodplug/lib/pkgconfig
- make
- make sdl
- sudo make install
- sudo make install_sdl
