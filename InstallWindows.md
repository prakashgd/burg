# Introduction #

This wiki shows how to compile BURG using msys+mingw environment.

# Prerequisite #

First, download python installer from:

http://www.python.org/download/

Use the latest package from 2.6 series.

Then, download bazaar from:

http://wiki.bazaar.canonical.com/WindowsDownloads

Standalone or python 2.6 based version are both all right.

After installation, add this to the PATH environment variable:

> C:\Python26;C:\Python26\Scripts

Finally, download burg\_msys development package from:

http://code.google.com/p/burg/downloads/list

And extract to any directory, for example c:\. It's a good idea to send a shortcut of msys.bat to desktop as you need to run this often.

# Build BURG #
I've created a few script to simplify the task of compiling BURG in Windows. First, launch a msys shell using msys.bat, then use these commands:

## burg\_dirs ##
This file set default build location. Here are their meanings:

SRCDIR is the path to source code, default value /c/burg/src.

OBJDIR is the path to object files, default value /c/burg/obj.

EOBJDIR is the path to object files for burg-emu, default value /c/burg/eobj.

BOOTDIR is the path to boot files, default value /c/burg/boot.

ISODIR is the path to iso root, default value /c/burg/iso.

BINDIR is the path to executable, default value /c/burg/bin.

Please note that msys use /c/ to represent c:\, and use forward slash instead of backward slash.

You can change build directory by editing this file.

## burg\_update ##
This command update the source code in SRCDIR to the latest version in launchpad.

If you run burg\_update for the first time, it may be a little slow because there are lots of revision to import. A trick is to download the latest burg-bzr package from http://code.google.com/p/burg/downloads/list, extract to C:\burg, and then run burg\_update. As burg-bzr package contains recent source tree, you only need to download the updates, which is much faster.

## burg\_compile ##
Incremental compile source code, use OBJDIR and EOBJDIR to store object files, the binaries are copied to BINDIR.

## burg\_rebuild ##
burg\_compile only compiles the necessary files, it's pretty fast for small change. But when there are lot of modification, burg\_compile could fail. In this case, you can use burg\_rebuild to purge the object files and then recompile.

## burg\_install ##
Copy module file from OBJDIR to BOOTDIR, also generate boot file buldr and buldr.mbr in the parent directory (c:/burg).

## burg\_mkiso ##
Copy modules file from OBJDIR to /boot/burg sub directory of ISODIR, and build bootable iso image burg.iso in the parent directory (c:/burg).

Here is an example work flow:

```
burg_update
burg_rebuild
burg_mkiso
```

# Enable graphic themes #

Download burg-themes package from:

http://code.google.com/p/burg/downloads/list

Extract to BOOTDIR (c:/burg/boot) or /boot/burg sub directory in ISODIR (c:/burg/iso/boot/burg), and write a configuration file burg.cfg in the same directory. For example:

```
set gfxmode=800x600
. ${prefix}/gui.cfg

menuentry "Boot Windows" --class windows {
  set root=(hd0,1)
  chainloader +1
  boot
}
```

# Live preview #
You can live preview the theme inside Windows, just click the burg-emu.bat batch file in BINDIR (c:/burg/bin).

# Config NT boot loader #
First, copy buldr and buldr.mbr to C:\.

For Windows NT/2000/XP/2003, add this line to the end of C:\boot.ini:

C:\buldr.mbr="Start BURG"

For Windows Vista/7, open a cmd windows with administrator privilege, then run this command:

```
bcdedit /create /d "Start BURG" /application bootsector 
```

It would display a guid, write it down. I use %guid% to represent it in the following examples. Enter the following commands:

```
bcdedit /set %guid% device boot
bcdedit /set %guid% path \buldr.mbr
bcdedit /displayorder %guid% /addlast 
```

That's it, you will see the "Start BURG" menu next time you boot windows.