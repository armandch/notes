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
- brew install ncurses pkg-config sdl2 sdl2_mixer freetype jpeg zlib libao libsndfile libsamplerate
- export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/opt/homebrew/opt/readline/lib/pkgconfig
- make
- make sdl
- sudo make install
- sudo make install_sdl

## Build frotz on CentOS 7.7
- `sudo yum install ncurses-devel libao-devel libmodplug-devel libsamplerate-devel libsndfile-devel libvorbis-devel SDL2-devel SDL2_mixer-devel freetype-devel libjpeg-turbo-devel`
- Update CFLAGS in Makefile to use optimized settings instead of debugging.
- Add `#include <stdint.h>` to `src/curses/ux_audio.c` to fix a bug with variable type.
- Build frotz with audio support: `make`.
- Install frotz: `sudo make install`.
- Build sfrotz: `make sdl`.
- Install sfrotz: `sudo make install_sdl`.


## Build SDL on CentOS 8
hg clone https://hg.libsdl.org/SDL SDL
cd SDL
mkdir build
cd build
../configure
make
sudo make install


## Build libogg
tar zxvf libogg-1.3.4.tar.gz
cd libogg-1.3.4
./configure
make
sudo make install

## Build libvorbis
tar zxvf libvorbis-1.3.6
cd libvorbis-1.3.6
./configure
make
sudo make install


## Build flac
tar Jxvf flac-1.3.2.tar.xz
cd flac-1.3.2
./configure
make
sudo make install


## Build mpg123
tar jxvf mpg123-1.25.13
cd mpg123-1.25.13
./configure
make
sudo make install


## Build opus
tar zxvf opus-1.3.1.tar.gz
cd opus-1.3.1
./configure
make
sudo make install


## Build opusfile
sudo dnf install openssl-devel
tar zxvf opusfile-0.11.tar.gz
cd opusfile-0.11
./configure
make
sudo make install


## Build SDL_mixer on CentOS 8
sudo dnf install libmodplug-devel fluidsynth-devel
hg clone https://hg.libsdl.org/SDL_mixer SDL_mixer
cd SDL_mixer
mkdir build
cd build
../configure
make
sudo make install


## Build libsndfile


## Build libsamplerate


## Build SDL Frotz on CentOS 8
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
./configure
make sdl
sudo make install install_sdl
