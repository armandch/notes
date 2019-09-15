# LDOS Y2K fix:
1. Use `TRSTools` to open LDOS boot disks.  It will automatically prompt to install Y2K fix.
2. `TRSTools` will install patches to the following versions of LDOS:
  - LDOS 5.3.1 for Model I
  - LDOS 5.3.1 for Model III
  - LDOS 6.3.1 for Model 4

# How to set up hard disk in LDOS:
1. Download hard disk utility disks for LDOS for Model I, III, and 4.
2. In emulator, create and insert a virtual hard disk file.
3. Boot into LDOS.
4. Load hard disk driver: `SYSTEM (DRIVE=4,DRIVER="RSHARD1")`.
5. (Optional) If hard disk has never been formatted before, format it: `RSFORM1A :4`.

# How to run BASIC programs:
1. Load BASIC: `BASIC`.
2. List programs in disk: `CMD"DIR :4"`.
3. Load program: `LOAD"ADVENT/BAS"`.
4. Run loaded program: `RUN`.
