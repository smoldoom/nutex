DeuTex
======

DeuTex can do many things with _Doom_, _Freedoom_, _Heretic_, _Hexen_,
and _Strife_ https://doomwiki.org/wiki/WAD[“WAD”] files, such as
extracting and inserting graphics, sounds, levels, and other
resources.  It can be used for creating and modifying IWAD (“Internal
WAD”) and PWAD (“Patch WAD”) files both.

It is a command-line driven program and as such, is suitable for
scripting such as from a shell script or Makefile.

File formats
------------

For insertion and extraction, DeuTex supports a few common formats.

For music, DeuTex supports both the DMX “mus” file format native to
_Doom_, and also MIDI files supported in _Doom_ 1.666 and newer.
There is no conversion between these formats, they are inserted and
extracted as-is.

For audio samples, they are saved and read using simple WAV files
containing only uncompressed PCM audio streams.

For the various forms of graphics, the BMP (uncompressed only), GIF,
PPM, and PNG footnote:[Requires libpng 1.6 or newer.] formats are
supported.

Unrecognized-format lumps are saved with +.lmp+ extension in the
+lumps+ directory and are re-inserted as-is from there.  Levels are
saved in an encapsulated PWAD file; breaking them apart would not be
useful for editing and all the lumps that make up a level are
co-dependent on each other.

Building and installing
-----------------------

DeuTex uses an Autoconf+Automake build system, so its compilation and
installation process is identical to most other Unix packages:

    ./configure
    make
    make install

When building directly from the version control repository, you will
need autoconf and automake installed and run the `./bootstrap` command
first to generate the `./configure` file.

To build and install the manpage, AsciiDoc must be installed, in
particular the DocBook-based `a2x` command for transforming it into
manpage format.  DeuTex will still build without it, however, and the
AsciiDoc source in +man/deutex.txt+ is fairly readable on its own.

To build and install on ReactOS or Microsoft Windows will require an
environment compatible with Unix shells and programs, such as
https://cygwin.com/[Cygwin] or http://www.msys2.org/[MSYS2].

History
-------

DeuTex began life as a fork of Doom Editing Utilities (known as DEU
for short) by Olivier Montanuy in 1994, expunging the graphical user
interface in favor of command line and scriptable usage scenarios.
Originally written for DOS, its primary home is now modern Unix and
Windows systems, and is a fundamental piece to building
_https://freedoom.github.io/[Freedoom’s]_ IWAD files.

The name comes from a play on LaTeX and in turn TeX, a popular
typesetting system in academia but no technical connection to DeuTex.
It is pronounced as two syllables, the first like “due” or “dew,” and
the second like “tech” (not “tex”!), owing from its namesake.

Copyright
---------

Copyright © 1994-1996 Olivier Montanuy, © 1999-2005 André Majorel, ©
2006-2021 contributors to the DeuTex project.

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or (at
your option) any later version.

This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR ANY PARTICULAR PURPOSE.  See the GNU
General Public License for more details, provided under the name
+COPYING+.
deutex

6

deutex

do things with wad files

**deutex** **-?**|**-h**|**-help**|**--help**

**deutex** **--version**

**deutex** \[*OPTIONS*\] **-add** *incomplete.wad* *out.wad*

**deutex** \[*OPTIONS*\] **-af** *flats.wad*

**deutex** \[*OPTIONS*\] **-append** *incomplete.wad*

**deutex** \[*OPTIONS*\] **-as** *sprite.wad*

**deutex** \[*OPTIONS*\] **-check** *in.wad*

**deutex** \[*OPTIONS*\] **-debug** \[*in.gif*\]

**deutex** \[*OPTIONS*\] **-get** *entry* \[*in.wad*\]

**deutex** \[*OPTIONS*\] **-join** *incomplete.wad* *in.wad*

**deutex** \[*OPTIONS*\] **-make** \[*dirctivs.txt*\] *out.wad*

**deutex** \[*OPTIONS*\] **-merge** *in.wad*

**deutex** \[*OPTIONS*\] **-pkgfx** \[*in.wad* \[*out.txt*\]\]

**deutex** \[*OPTIONS*\] **-pknormal** \[*in.wad* \[*out.txt*\]\]

**deutex** \[*OPTIONS*\] **-restore**

**deutex** \[*OPTIONS*\] **-usedidx** \[*in.wad*\]

**deutex** \[*OPTIONS*\] **-usedtex** \[*in.wad*\]

**deutex** \[*OPTIONS*\] **-unused** *in.wad*

**deutex** \[*OPTIONS*\] **-wadir** \[*in.wad*\]

**deutex** \[*OPTIONS*\] **-xtract** *in.wad* \[*dirctivs.txt*\]

DESCRIPTION
===========

DeuTex is a wad composer for Doom, Heretic, Hexen and Strife. It can be
used to extract the lumps of a wad and save them as individual files or
the reverse, and much more.

When extracting a lump to a file, it does not just copy the raw data, it
converts it to an appropriate format (such as PPM for graphics, Sun
audio for samples, etc.). Conversely, when it reads files for inclusion
in pwads, it does the necessary conversions (for example, from PPM to
Doom picture format).

Decomposing a wad
-----------------

To decompose a wad (i.e. extract its contents), use the **-extract**
(a.k.a. **-xtract**) command. When decomposing a wad, DeuTex creates one
file for each lump. The files are created in one of the following
subdirectories of the working directory: **flats/**, **lumps/**,
**musics/**, **patches/**, **sounds/**, **sprites/**, **textures/**. The
decomposing process also creates a very important file, **wadinfo.txt**,
which will be used later when composing.

To extract the contents of the Doom II iwad,

    deutex -doom2 /path/to/doom2.wad -xtract

To extract the contents of a Doom II pwad named mywad.wad,

    deutex -doom2 /path/to/doom2.wad -xtract mywad.wad

To extract only the sprites,

    deutex -doom2 /path/to/doom2.wad -sprites -xtract

To extract only the sounds,

    deutex -doom2 /path/to/doom2.wad -sounds -xtract

Composing (building) a wad
--------------------------

Composing is the symmetrical process. It’s done with the three commands
**-build**, **-create** and **-make**, that are equivalent. Using
**wadinfo.txt** and the files in **flats/**, **lumps/**, **musics/**,
**patches/**, **sounds/**, **sprites/** and **textures/**, DeuTex
creates a new wad.

To create a new pwad named mywad.wad,

    deutex -doom2 /path/to/doom2.wad -make mywad.wad

To create a new iwad named mytc.wad,

    deutex -doom2 /path/to/doom2.wad -iwad -make mytc.wad

Other operations
----------------

DeuTex has many (too many?) other commands like **-join**, **-merge**,
**-usedtex** etc.

OPTIONS
=======

Modal options not requiring an iwad
-----------------------------------

**-?**, **-h**, **-help**, **--help**
Print list of options.

**-syntax**
Print the syntax of wad creation directives.

**--version**
Print version number and exit immediately.

**-unused** *in.wad*
Find unused spaces in a wad.

Modal options requiring an iwad
-------------------------------

**-add** *in.wad* *out.wad*
Copy sp & fl of iwad and *in.wad* to *out.wad*.

**-af** *flats.wad*
Append all floors/ceilings to the wad.

**-append** *io.wad*
Add sprites & flats of iwad to io.wad.

**-as** *sprite.wad*
Append all sprites to the wad.

**-build**|**-create**|**-make** \[*in.txt*\] *out.wad*
Make a pwad.

**-check**|**-test** *in.wad*
Check the textures.

**-debug** \[*file*\]
Debug color conversion.

**-extract**|**-xtract** \[*in.wad* \[*out.txt*\]\]
Extract some/all entries from a wad.

**-get** *entry* \[*in.wad*\]
Get a wad entry from main wad or in.wad.

**-join** *incomplete.wad* *in.wad*
Append sprites & flats of Doom to a pwad.

**-merge** *in.wad*
Merge doom.wad and a pwad.

**-pkgfx** \[*in.wad* \[*out.txt*\]\]
Detect identical graphics.

**-pknormal** \[*in.wad* \[*out.txt*\]\]
Detect identical normal.

**-restore**
Restore doom.wad and the pwad.

**-usedidx** \[*in.wad*\]
Color index usage statistics.

**-usedtex** \[*in.wad*\]
List textures used in all levels.

**-wadir** \[*in.wad*\]
List and identify entries in a wad.

General options
---------------

**-overwrite**
Overwrite all.

**-dir** *dir*
Extraction directory (default `.`).

Iwad
----

**-doom** *dir*
Path to Doom iwad.

Wad options
-----------

**-be**
Assume all wads are big endian (default LE).

**-deu**
Add 64k of junk for DEU 5.21 compatibility.

**-george**|**-s\_end**
Use **S\_END** for sprites, not **SS\_END**.

**-ibe**
Input wads are big endian (default LE).

**-ile**
Input wads are little endian (default).

**-ipf** *code*
Picture format (**alpha**, **normal**, **pr**; default normal).

**-itf** *code*
Input texture format (**nameless**, **none**, **normal**, **strife11**;
default normal).

**-itl** *code*
Texture lump (**none**, **normal**, **textures**; default normal).

**-iwad**
Compose iwad, not pwad.

**-le**
Assume all wads are little endian (default).

**-obe**
Create big endian wads (default LE).

**-ole**
Create little endian wads (default).

**-otf** *code*
Output texture format (**nameless**, **none**, **normal**, **strife11**;
default normal).

**-pngoffsets**
Override offsets in WADINFO with offsets contained in PNG metadata

**-tf** *code*
Texture format (**nameless**, **none**, **normal**, **strife11**;
default normal).

Lump selection
--------------

**-flats**
Select flats.

**-graphics**
Select graphics.

**-levels**
Select levels.

**-lumps**
Select lumps.

**-musics**
Select musics.

**-patches**
Select patches.

**-scripts**
Select Strife scripts.

**-sneas**
Select sneas (sneaps and sneats).

**-sneaps**
Select sneaps.

**-sneats**
Select sneats.

**-sounds**
Select sounds.

**-sprites**
Select sprites.

**-textures**
Select textures.

Graphics
--------

**-bmp**
Save pictures as BMP (**.bmp**).

**-png**
Save pictures as PNG (**.png**). Default format.

**-gif**
Save pictures as GIF (**.gif**).

**-ppm**
Save pictures as rawbits PPM (P6, **.ppm**).

**-rgb** *r* *g* *b*
Specify the transparent colour (default 0 47 47).

Sound
-----

**-rate** *code*
Policy for != 11025 Hz (**reject**, **force**, **warn**, **accept**;
default warn).

Reporting
---------

**-di** *name*
Debug identification of entry.

**-v0**|**-v1**|**-v2**|**-v3**|**-v4**|**-v5**
Set verbosity level, default 2.

DIAGNOSTICS
===========

All messages are identified by a unique code. Some messages are
identical; the code is useful to distinguish them. All codes have four
characters: two letters and two digits. The letters identify the part of
the code where the message comes from, the digits give the message
number within that area. In general, numbers are assigned so that
messages that come from parts of the code that are executed earlier have
lower numbers.

FILES
=====

*dir***/flats/**
When extracting, flats are saved to this directory. When composing,
flats are read from this directory.

*dir***/graphics/**
When extracting, graphics are saved to this directory. When composing,
graphics are read from this directory.

*dir***/levels/**
When extracting, levels are saved to this directory. When composing,
levels are read from this directory.

*dir***/lumps/**
When extracting, lumps are saved to this directory. When composing,
lumps are read from this directory.

*dir***/musics/**
When extracting, musics are saved to this directory. When composing,
musics are read from this directory.

*dir***/patches/**
When extracting, patches are saved to this directory. When composing,
patches are read from this directory.

*dir***/scripts/**
When extracting, Strife scripts are saved to this directory. When
composing, Strife scripts are read from this directory.

*dir***/sneaps/**
When extracting, Doom alpha sneaps are saved to this directory. When
composing, Doom alpha sneaps are read from this directory.

*dir***/sneats/**
When extracting, Doom alpha sneats are saved to this directory. When
composing, Doom alpha sneats are read from this directory.

*dir***/sounds/**
When extracting, sounds are saved to this directory. When composing,
sounds are read from this directory.

*dir***/sprites/**
When extracting, sprites are saved to this directory. When composing,
sprites are read from this directory.

*dir***/textures/texture1.txt**
The **TEXTURE1** lump (all but Doom alpha 0.4 and 0.5).

*dir***/textures/texture2.txt**
The **TEXTURE2** lump (all commercial IWADs except Doom 2).

*dir***/textures/textures.txt**
The **TEXTURES** lump (Doom alpha 0.4 and 0.5).

*dir***/tx\_start/**
Special texture directory for certain engines such as ZDoom. Specifying
a positive integer after the name in wadinfo.txt causes no format
conversion to be performed (eg, PNGs and BMPs remain as PNGs and BMPs in
the WAD), otherwise an attempt to convert to Doom’s patch format is
done.

*dir***/wadinfo.txt**
The default master file.

ENVIRONMENT
===========

**DOOMWADDIR**
The directory where the iwad resides. The value of this environment
variable is overridden by **-main**, **-doom** and friends.
