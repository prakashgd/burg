# GRUB\_DEFAULT #
Value: menu item index (0 based) or saved<br>
Default: 0<br>
<br>
This variable configures the default menu item. When its value is saved, it uses the one stored in burgenv as default. Please note that to achieve the save default effect, you need to set GRUB_DEFAULT to saved, and GRUB_SAVEDEFAULT to true.<br>
<br>
<h1>GRUB_HIDDEN_TIMEOUT</h1>
Value: any string to indicate true, empty string to indicate false.<br>
Default: empty string (false)<br>
<br>
If this variable is true, it would not display timeout in menu, but sleep silently. You can use ESC key to interrupt the sleep and display menu normally.<br>
<br>
<h1>GRUB_HIDDEN_TIMEOUT_QUIET</h1>
Value: true or false.<br>
Default: false<br>
<br>
This variable works in conjunction with GRUB_HIDDEN_TIMEOUT. When it's true, the hidden timeout is completely silently, otherwise it shows the countdown.<br>
<br>
<h1>GRUB_TIMEOUT</h1>
Value: timeout in seconds<br>
<br>
This variable set the timeout value. If it's not set, timeout is infinity.<br>
<br>
<h1>GRUB_DISTRIBUTOR</h1>
Value: the name of current Linux distribution<br>
<br>
You can use lsb_release command to extract distribution information, for example:<br>
<pre><code>GRUB_DISTRIBUTOR=`lsb_release -i -s 2&gt; /dev/null || echo Debian`<br>
</code></pre>

<h1>GRUB_CMDLINE_LINUX and GRUB_CMDLINE_LINUX_DEFAULT</h1>
Value: command line parameter for Linux kernel<br>
<br>
The difference between GRUB_CMDLINE_LINUX and GRUB_CMDLINE_LINUX_DEFAULT is that GRUB_CMDLINE_LINUX is used in both normal and rescue boot items, while GRUB_CMDLINE_LINUX_DEFAULT is only used in normal boot items.<br>
<br>
<h1>GRUB_TERMINAL_INPUT, GRUB_TERMINAL_OUTPUT and GRUB_TERMINAL</h1>
Value: serial, console or gfxterm<br>
Default: gfxterm<br>
<br>
The input and output terminal driver to use. If input and output driver is the same, you can use GRUB_TERMINAL to set them both. If they're not set, it would try to use gfxterm if video mode is available.<br>
<br>
<h1>GRUB_FONT</h1>
Value: path to font file<br>
<br>
If this is not set, it will scan /boot/burg and /usr/share/burg directory for file unicode.pf2, unifont.pf2 or ascii.pf2 and use the first one found as default font file. If none is found, it will use console terminal instead of gfxterm as default.<br>
<br>
<h1>GRUB_SERIAL_COMMAND</h1>

This variable specify the command to setup serial console.<br>
<br>
<h1>GRUB_DISABLE_LINUX_UUID</h1>
Value: true or false<br>
Default: false<br>
<br>
If this variable is true, it would use device name in Linux kernel parameter, such as root=/dev/sda1, instead of root=UUID=...<br>
<br>
<h1>GRUB_DISABLE_LINUX_RECOVERY</h1>
Value: true or false<br>
Default: false<br>
<br>
If this variable is true, it won't generate Linux boot items for rescue mode.<br>
<br>
<h1>GRUB_GFXMODE</h1>
Value: graphic mode screen resolution<br>
Default: 640x480<br>
<br>
You can use vbeinfo command in console windows to find out what modes are supported by video bios.<br>
<br>
<h1>GRUB_THEME</h1>
Value: theme name or saved (BURG), or path of grub2 theme file (GRUB2)<br>
<br>
If you use BURG themes, set this to the name of theme, or saved, which means to use the last selected theme. At run-time, you can use 't' hot-key to open a theme selection box and change theme dynamically. If you use GRUB2 themes, set this as the path of theme file.<br>
<br>
<h1>GRUB_GFXPAYLOAD_LINUX</h1>
Value: keep, text or video mode such as 640x480<br>
Default: keep<br>
<br>
This variable configures the video mode before switching to Linux. keep means keep the current video mode, text means switch back to text mode. You can use this variable to avoid unnecessary mode switch.<br>
<br>
<h1>GRUB_DISABLE_OS_PROBER</h1>
Value: true or false<br>
Default: false<br>
<br>
If it's true, don't run os-prober to detect additional OS.<br>
<br>
<h1>GRUB_INIT_TUNE</h1>
Value: parameter for the play command<br>
<br>
If this is set, it would play an initial tune.<br>
<br>
<h1>GRUB_SAVEDEFAULT</h1>
Value: true or false<br>
Default: false<br>
<br>
If it's true, save the current selected menu entry to burgenv so that it can be read back at next boot.<br>
<br>
<h1>GRUB_FOLD (BURG only)</h1>
Value: true, false or saved<br>
Default: false<br>
<br>
You can have normal and rescue boot item for the same kernel, and much more if you have multiple kernels installed. With this variable, you can fold them into one so that it would be easier to select other OS. You can always use 'f' hot-key to switch between folding and unfolding mode. In folding mode, you can also use 'F7' hot-key to pop-up a menu to see the folded items. If this variable is set to saved, it would use the previous selection as default.<br>
<br>
<h1>GRUB_USERS (BURG only)</h1>

This variable configures password protection for boot items, see <a href='Authentication.md'>Authentication</a> for more information.<br>
<br>
<h1>GRUB_LINUX16 (BURG only)</h1>
Value: true or false<br>
Default: false<br>
<br>
When this is set to true, it'd use the old real mode Linux loader linux16/initrd16 instead of the new protected mode loader.<br>
<br>
<h1>GRUB_TITLE_OVERRIDE (BURG only)</h1>

This variable is used to change the menu title of OS detected by os-prober, for example:<br>
<pre><code>GRUB_TITLE_OVERRIDE="/dev/sda5=Windows 1:/dev/sda6=Windows 2"<br>
</code></pre>

<h1>GRUB_CLASS_OVERRIDE (BURG only)</h1>

Similar to GRUB_TITLE_OVERRIDE, but this one change OS class. It can be used to set customized icons for selected partition.<br>
<pre><code>GRUB_CLASS_OVERRIDE="/dev/sda5=win1:/dev/sda6=win2"<br>
</code></pre>