To convert game data binary of this directory to C header files.

- DOOM.WAD -> doombin.h
- prboom.wad -> prboombin.h

Please run cmake to convert.

$ ninja -C build all

And put generated headers (doombin.h and prboombin.h) are in build/include/ directory to prboom2/src/ directory.
