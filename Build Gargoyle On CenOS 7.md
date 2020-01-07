# Install jam
 - [Download source code](https://swarm.workshop.perforce.com/files/guest/perforce_software/jam/src)

# Install smpeg
 - `svn co svn://svn.icculus.org/smpeg/trunk smpeg`

# Install dependencies
 - `sudo yum install SDL-devel SDL_mixer-devel SDL_sound-devel`

# Build Gargoyle
 - `git clone git@github.com:garglk/garglk.git`
 - `cd garglk`
 - `jam`
 - `jam install`
 - `sudo env SYSTEM=1 jam install`
 - `sudo ln -s -f /usr/local/libexec/gargoyle/gargoyle /usr/local/bin/gargoyle`
 - `sudo ln -s -f /usr/local/lib/gargoyle/libgarglk.so /usr/lib64/libgarglk.so`
 - `sudo cp garglk/garglk.ini /etc/garglk.ini`
