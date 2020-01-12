# Convert Infocom Story Files To Run In Official Infocom Interpreter

## Border Zone, the only game Infocom did not release on Amiga

### Official Infocom Amiga Interpreter
- Border Zone can be run by official Infocom interpreter version `5A`. Copy this interpreter from Beyond Zork.
- Verify the size of interpreter: `wc -c < Beyond\ Zork`. The size should be `37148` bytes.
- Rename interpreter name from `Beyond Zork` to `Border Zone`.

### Story File
- Download Border Zone story file Release 9 Serial 871008.
- Unfortunately, the official Infocom Amiga interpreter only loads story file size of 256/512K bytes.
- Count bytes of story file: `wc -c < borderzone-r9-s871008.z5`. Result is `178372`. We should pad bytes to the end of this story file.
- Verify the total number of bytes we need by counting byte number from story file of Beyond Zork: `wc -c < Beyond\ Zork`. The result is `261632`.
- We have to append `261632 - 178372 = 83260` bytes to the end of the story file of Border Zone.
- Padding missing bytes: `dd if=/dev/zero bs=1 count=83260 >> borderzone-r9-s871008.z5`.
- Verify total number of bytes is correct now: `wc -c < borderzone-r9-s871008.z5`. The result should be `261632` now.
- Rename story file from `borderzone-r9-s871008.z` to `Story.Data`.

### Now You Should Be Able To Run Border Zone Using Official Infocom Amiga Interpreter!