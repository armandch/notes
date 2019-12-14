## Hardfile in RDB mode
- `DF1:HDTools/HDToolBox uaehf.device`

## LhA
- `Ram:`
- `Tools:lha.run`
- `Copy lha_68020 C:LhA`

## LZX
- `Ram:`
- `lha x Tools:spatch.lha Ram:`
- `Copy Ram:spatch/spatch.68k C:spatch`
- `lha x Tools:lzx121r1.lha Ram:`
- `lha x Tools:LZX_Y2Kfix.lha Ram:`
- `spatch -o LZX -p LZX_68020r.pch LZX_68020r`
- `Copy LZX C:LZX`
- `Copy LZX.Keyfile L:lzx.keyfile`
- `Delete C:spatch`

## Instsaller
- `Ram:`
- `lha x Tools:NDK39.lha Ram:`
- `Copy NDK39/Tools/Installer/Installer System:Utilities/Installer`

## Info-Zip Unzip
- `S:Startup-Sequence`: setenv TZ EST5EDT

## KingCON

## MUI

## ClassAct

## (Optional) Picasso96

## (Optional) NewIcons

## (Optional) Scalos

## (Optional) MagicWB

## (Optional) WHDLoad

## (Tools) Redit

## (Tools) WhichAmiga