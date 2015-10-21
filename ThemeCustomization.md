# Introduction #

Themes are stored in /boot/burg/themes directory. You can modify them directly, but the changes would be overwritten when you update burg-themes package. This wiki shows how to make customization that can survive updates.

# Add/Change OS icon #

You can add new icon for new OS class, or change an existing one. You can use the following files to specify customized icons:

  * /boot/burg/themes/custom/icon\_large - Large icons, used by refit theme.
  * /boot/burg/themes/custom/icon\_hover - Large icon for selected item, grey icon for others, used by sora and radiance theme.
  * /boot/burg/themes/custom/icon\_grey - Grey icons, used by black\_and\_white and coffee theme.
  * /boot/burg/themes/custom/icon\_small - Small icons, used by the rest themes.

You also need to copy icons to /boot/burg/themes/custom/ directory.

Here is an example to add a new OS class myos:

icon\_small:
```
+class {
  -myos { image = "$$/small_icon.png" }
}
```

icon\_large:
```
+class {
  -myos { image = "$$/large_icon.png" }
}
```

icon\_hover:
```
+class {
  -myos { image = "$$/grey_icon.png:$$/large_icon.png" }
}
```

icon\_grey:
```
+class {
  -myos { image = "$$/grey_icon.png" }
}
```

The size of large icon is 128 x 128. BURG only support RGB png, you need to convert it if it uses indexed color or greyscale.

The size of small icon is 24 x 24, you can generate it by scaling down the large icon.

The size of grey icon is 128 x 128, here is the process to generate it from large icon using GIMP:

  1. Open the large icon in GIMP.
  1. Click menu "Image->Mode->Greyscale", this convert it to black and white image.
  1. Click menu "Image->Mode->RGB". BURG don't support greyscale format, so you need to change the mode back to RGB.
  1. Click menu "Image->Scale Image...", scale the image size to 90 x 90.
  1. Click menu "Image->Canvas Size...". In "Canvas Size" part, set width and height to 128. In "Offset" part, click "Center". Then click "Resize" at the bottom.
  1. Click menu "File->Save as". In the dialog about PNG plug-in can't handle layer offsets, size or opacity, use "Export".

# Customize themes #

For example, to change the background image of refit theme, you can use this:

/boot/burg/themes/custom/theme\_refit:
```
+screen {
  background = "$$/desktop.png"
}
```

The image file desktop.png needed to be copied to /boot/burg/themes/custom/ directory.