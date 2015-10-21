# BURG fails to start after I boot into Windows #

This happens mostly to Dell machines. The root cause of this issue is that some program writes information at the beginning of disk, which overwrites part of the multi-sector BURG MBR. The solution is to use alternative install mode that uses only one sector MBR which is guaranteed to be safe.

You can boot into rescue CD, open a rescue shell on the original root device, and use something like this to install BURG to MBR:
```
burg-install --alt /dev/sda
```
The option --alt indicates alternative install mode.

# BURG works, but it hangs when I try to boot Linux #

This could be caused by the protected mode Linux loader, you can try the old real mode loader linux16/initrd16. Boot into rescue shell, add this settings to /etc/default/burg:

```
GRUB_LINUX16=true
```

Then use update-burg to generate a new burg.cfg.

# My issue is not listed here, where do I ask for help #
You can post a thread at the BURG forum:

http://www.burgloader.com/bbs/