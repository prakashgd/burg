# Wubi install #

If you install ubuntu using wubi, follow steps in this section. Otherwise, jump to the next section.

First, download the latest burg\_wubi package from the download area, and extract to C:\ubuntu\ directory.

To enable graphic menu, download the latest burg-themes package from download area, and extract to C:\ubuntu\burg\ directory.

Then, copy C:\ubuntu\burg\wubildr to C:\ and overwrite the old file.

That's it, it will display BURG menu next time you start wubi from NT loader.

To restore the original loader, just copy C:\ubuntu\winboot\wubildr to C:\.

BTW, you may notice that all OS uses the unknown icon, this is because wubildr rely on /boot/grub/grub.cfg to add menu items, but grub.cfg don't have the --class option which is required to display OS icon properly. This is easy to fix. Login ubuntu, copy 10\_lupin and 30\_os-prober from /host/ubuntu/burg/ directory to /etc/grub.d/, then run update-grub to generate a new grub.cfg.

# Normal install #
Here are the steps to install BURG using PPA package from launchpad.

1. Insert these lines to /etc/apt/sources.list

```
deb http://ppa.launchpad.net/bean123ch/burg/ubuntu lucid main
deb-src http://ppa.launchpad.net/bean123ch/burg/ubuntu lucid main
```

You should replace lucid with the correct code name. Currently the following release are supported: jaunty (9.04), karmic (9.10), lucid (10.04), maverick (10.10).

And install burg and related themes using these commands:
```
sudo apt-get update
sudo apt-get install burg
```

If you want to avoid the warning about unknown signature, use these commands to import it:
```
gpg --keyserver keyserver.ubuntu.com --recv 55708F1EE06803C5
gpg --export --armor 55708F1EE06803C5 | sudo apt-key add -
```

Then, install burg to MBR with the following command:
```
sudo burg-install /dev/sda
sudo update-burg
```
Change hd0 if you want to install to other disk.

2. Edit configuration file /etc/default/burg

For the latest version, you don't need to modify /etc/default/burg at all. If you upgrade from previous version, it's recommended to change the setting of GRUB\_THEME and GRUB\_FOLD to:

```
GRUB_THEME=saved
GRUB_FOLD=saved
```

This allows you to change theme and folding options dynamically.

Here are the hot-keys defined in the boot menu:

  * t - Open theme selection menu
  * f - Toggle between folding mode
  * n - Jump to the next item with the same class
  * w - Jump to the next Windows item
  * u - Jump to the next Ubuntu item
  * e - Edit the command of current boot item
  * c - Open a terminal window
  * 2 - Open two terminal windows
  * h - Display help dialog (only available in sora theme)
  * i - Display about dialog (only available in sora theme)
  * q - Return to old grub menu
  * F5/ctrl-x - Finish edit
  * F6 - Switch window in dual terminal mode
  * F7 - List the folded boot items
  * F8 - Toggle between graphic and text mode
  * F9 - shutdown
  * F10 - reboot
  * ESC - quit from the current popup menu or dialog.

Since 20100309 version, burg also supports grub2 theme. To try it, set GRUB\_THEME to the name of the theme file, and run update-burg. Currently only one grub2 theme is available in burg-themes package:

```
GRUB_THEME=/boot/burg/themes/debian-theme/theme.txt
```

Screenshots: [Screenshots](Screenshots.md)

3. Live preview themes in host OS

To preview the current configuration, use this command:
```
sudo burg-emu
```

grub2 theme needs to access disk directly, to preview it, you need to add -D option:
```
sudo burg-emu -D
```

4. Troubleshooting

If you encounter issue with BURG, try the tips in [Troubleshooting](Troubleshooting.md)