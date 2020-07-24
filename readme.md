# Game Boy Debug Monitors
These are partial gameboy roms recovered from an official Nintendo Game Boy emulator. The raw data comes from `/turnout/gbemu_rvl/src/GBEmulator.cpp`.

The partial roms are patched in over an existing rom in memory, and as such do not have headers and cannot be run directly. I put together a minimal rom using tutorial code and patched in the monitor roms. There are three: one for original gameboy (DMG), one for gameboy pocket (MGB) and one for gameboy color (CGB). There are three files for the color one. `monitorromCGB.rom` is the full color monitor exactly as specified in the source. However, it can't be simply patched into a rom file because it would overwrite the entry point with a block of all zeroes. `monitorromCGB-A.rom` goes before the entry point at `0x0000` and `monitorromCGB-B.rom` goes after the entry point at `0x0200`.


So, what do they do? \*drumroll\*... they loop the boot logo. Yep. That's it. The color rom is visually glitchy, presumably because something is wrong with the header (not sure what to change). But it clearly has the same functionality as the other two.

When a flag is set in the emulator, these partial roms are written over the loaded rom. Presumably these are a basic debug tool to verify whether the problem is the rom or the emulator.