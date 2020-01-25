# Create AmigaOS 3.1 Installation

## Hardfile in RDB mode
- `DF1:HDTools/HDToolBox uaehf.device`

## Install BetterWB 4.3
- [BetterWB Website](http://lilliput.amiga-projects.net/BetterWB.htm)
- Install BetterWB 4.0 first.
- During installation, when asked about enabling `ENV-HANDLER` plugin, say `No`.
- Upgrade BetterWB to 4.3.

## Update LhA
- The LhA version comes with BetterWB is `v2.15 68000+`. I want to install `v2.15 68020+` CPU specific version.
- `Ram:`
- `Tools:lha.run`
- `COPY lha_68020 C:LhA`

## Install KingCON
- `LhA x Tools:KingCON_1.3.lha Work:Temp/`
- Run KingCON installer.
- Edit `S:user-startup`:
`
Assign CON: DISMOUNT
Assign RAW: DISMOUNT

MOUNT CON: from DEVS:KingCON-mountlist
MOUNT RAW: from DEVS:KingCON-mountlist
`
- Reboot.

## Update Redit
- The Redit application comes with BetterWB is version `1.16`. I want to update it to version `2.0`.
- `LhA x Tools:Redit.lha Work:Temp/`
- `COPY Work:Temp/Redit2.0/Redit TO C:Redit`
- `COPY Work:Temp/Redit2.0/readme TO HELP:Redit.txt`

## Update LZX
- The LZX version comes with BetterWB is `1.21 68000/68010`. I want to install `1.21 68020/68030` CPU specific version and patch the Y2K bug.
- `LhA x Tools:spatch.lha Work:Temp/`
- `COPY Work:Temp/spatch/spatch.68k C:spatch`
- `MAKEDIR Work:Temp/lzx`
- `LhA x Tools:lzx121r1.lha Work:Temp/lzx/`
- `LhA x Tools:LZX_Y2Kfix.lha Work:Temp/lzx/`
- `CD Work:Temp/lzx`
- `spatch -o LZX -p LZX_68020r.pch LZX_68020r`
- `COPY LZX C:LZX`
- `COPY LZX.Keyfile L:lzx.keyfile`
- `DELETE C:spatch`

## Update Info-Zip UnZip
- The UnZip version comes with BetterWB is `5.41`. I want to update it to `5.50`.
- `MAKEDIR Work:Temp/unzip`
- `LhA x Tools:unz550xA.lha Work:Temp/unzip/`
- `COPY fUnZip MakeSFX UnZip UnZipSFX C:`
- Fix UnZip timezone warning: Edit `S:Startup-Sequence` file and put this line in: `setenv TZ EST5EDT`.

## Update Instsaller
- `LhA x Tools:NDK39.lha Work:Temp/`
- `COPY Work:Temp/NDK_39/Tools/Installer/Installer System:Utilities/Installer`
- `COPY Work:Temp/NDK_39/Tools/Installer/Installer.guide HELP:Installer.guide`

## Install MUI
- `LhA x Tools:MUI/mui38usr.lha Work:Temp/`
- `CD Work:Temp/`
- `UnZip Tools:MUI/MUIKey.zip`
- `COPY MUI.KEY S:MUI.KEY`
- Run MUI installer.
- Reboot.
- Launch MUI, go to `Project > Open`, then select `Stuntzi.prefs` and save.
- Reboot.

## Install HighGFX
- `LhA x Tools:HighGFX40_6.lha Work:Temp/`
- `COPY Work:Temp/HighGFX40_6/HighGFX System:Devs/Monitors/`
- `COPY Work:Temp/HighGFX40_6/HighGFX.info System:Devs/Monitors/`
- `COPY Work:Temp/HighGFX40_6/Bonus/HD720 System:Devs/Monitors/`
- `COPY Work:Temp/HighGFX40_6/Bonus/HD720.info System:Devs/Monitors/`

## Install ClassAct
- `LhA x Tools:ClassAct/ClassAct2Demo.lha Work:Temp/`
- Run ClassAct installer.
- `LhA x Tools:ClassAct/classact33.lha System:` Overwrite all files when prompted, except for the two `.info` files.
- `RENAME System:Prefs/CAPrefs.doc TO HELP:CAPrefs.doc`
- `DELETE System:Prefs/CAPrefs.doc.info`
- `RENAME System:Prefs/classact.history TO HELP:ClassAct.history`
- `DELETE System:Prefs/ClassAct.history.info`
- Reboot.

## Update IconLib
- The IconLib comes with BetterWB is not CPU specific version. I want to install `68020` CPU specific version.
- `LhA x Tools:IconLib_46.4.lha Work:Temp/`
- `COPY Work:Temp/IconLib_46.4/Libs/icon.library_68020 System:Libs/icon.library`
- `COPY Work:Temp/IconLib_46.4/C/ System:C/`
- Reboot.

## Configure Glow Icons
- Launch `System:Prefs/IconSet` and select the Glow Icons option.
- Run `System:Prefs/FullPalette` to enable full palette.
- Enable `DontShowIBorder` and `SwazInfo` commodities.
- Reboot.
- Launch `System:Tools/IconEdit`, open `System:Prefs/Presets/IconSets/Glowicons.info` icon file and save it as default icon.
- (Optional) You can also install `AB-GlowIcons_Suite` for more icon sets: `LhA x PC:AB-GlowIcons_Suite.lha System:Prefs/Presets/IconSets/`.
- Use `CopyIcon` tool to copy icons.

## Enable Commodities
- Launch `System:Prefs/WBStartup`.
- Enable the followings: `DontShowIBorder`, `MagicMenu`, `CleverWIN`, `SwazInfo`, `FreeWheel`, `PowerSnap`, `AltTab`, `Ned`, `IconAppearer`, `WindowToFront`.

## Install FBlit
- `lha x Tools:fblit.lha Work:Temp/`
- `COPY Work:Temp/FBlit/FBlit System:C/FBlit`
- `COPY Work:Temp/FBlit/FBlit.info System:C/FBlit.info`
- `COPY Work:Temp/FBlit/FBlitGUI System:C/FBlitGUI`
- `COPY Work:Temp/FBlit/fblit.library System:Libs/fblit.library`
- `COPY Work:Temp/FBlit/FBlit.guide HELP:FBlit.guide`
- Reboot.

## Install MCP 1.30
- `LhA x Tools:MCP130.lha Work:Temp/`
- Run MCP installer.
- Reboot.

## (Alternative) Install MCP 1.48
- `LhA x Tools:ScreenNotify10.lha Work:Temp/`
- `COPY Work:Temp/ScreenNotify/libs/screennotify.library LIBS:screennotify.library`
- `COPY Work:Temp/ScreenNotify/libs/screennotify.doc HELP:screennotify.doc`
- `LhA x Tools:MCC_NList-0.125.lha Work:Temp/`
- `COPY Work:Temp/MCC_NList/Libs/MUI/AmigaOS3/#?.mcc MUI:Libs/mui/`
- `COPY Work:Temp/MCC_NList/Libs/MUI/AmigaOS3/#?.mcp MUI:Libs/mui/`
- `LhA x Tools:mcp1_48.lha Work:Temp/`
- Run MCP installer.
- Reboot.

## Install Dopus 4.16
- `LhA x Tools:DOpus416JRbin.lha Work:Temp/`
- Run DOpus installer.

## Install WHDLoad 18.5
- Copy Kickstarts to `System:Devs/Kickstarts/`.
- `LhA x Tools:WHDLoad_usr.lha Work:Temp/`
- Run WHDLoad installer.

## Install ToolMaster 3.1
- `LhA x Tools:icondt.lha Work:Temp/`
- `COPY Work:Temp/icon.datatype System:Classes/Datatypes/`
- `COPY Work:Temp/Icon System:Devs/Datatypes/`
- `COPY Work:Temp/Icon.info System:Devs/Datatypes/`
- `COPY Work:Temp/icondt.readme HELP:`
- `LhA x Tools:ToolManagerBin.lha Work:Temp/`
- `LhA x Tools:ToolManagerExt.lha Work:Temp/`
- `LhA x Tools:DockBrushes.lha System:Prefs/Presets/`
- Run ToolMaster installer.
- Reboot.
- Configure your dock. You can reference [here](http://www.mfilos.com/2012/04/guide-install-configure-lightweight-dock.html).

## (Optional) QBoot
- `LhA x Tools:qboot.lha Work:Temp/`
- `CD Work:Temp/qboot-1.07`
- `COPY qboot qboot.conf #?.loco S:`
- Edit `S:startup-sequence` and add the following line immediately after `C:SetPatch`: `S:qboot "****"`.
- Tinker `S:qboot.conf` if you want.
- Reboot.

## (Optional) Install SysInfo
- `LhA x Tools:SysInfo.lha Work:Softwares/`

## (Optional) Install FileX
- `LhA x Tools:FileX-68K.lha Work:Softwares/`

## (Optional) Picasso96

## (Optional) NewIcons

## (Optional) Scalos

## (Optional) MagicWB