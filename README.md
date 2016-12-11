# be-mac
XKB keymap file for Belgian Macs

This keymap is not complete, but the most important characters (those visible on the keys and/or important for code) should work correctly.

The `be` file is a copy of the original file, to which I added a new `mac` variant, based on the basic layout. It should be placed in `/usr/share/X11/xkb/symbols`.  
The `evdev.lst` and `evdev.xml` are updated versions to make sure the system can find the new variant and should both be placed in `/usr/share/X11/xkb/rules`.

## Installation
### Backup
Before you do anything, make a backup of the files you're going to overwrite:
  * `/usr/share/X11/xkb/symbols/be`
  * `/usr/share/X11/xkb/rules/evdev.lst`
  * `/usr/share/X11/xkb/rules/evdev.xml`

Example command (don't type the `$`):
```
$ rm /usr/share/X11/xkb/symbols/be /usr/share/X11/xkb/rules/evdev.lst /usr/share/X11/xkb/rules/evdev.xml
```
You may have to prepend `sudo` or `gksu` and type your password to make this work.

### Copy files
First, clone this repository, either by downloading the .zip file or by using git:
```
$ git clone git@github.com:TuurDutoit/be-mac.git
```

Then, install the keymap, by copying the files like so (make sure you're in the repo's directory):
```
$ cp be /usr/share/X11/xkb/symbols
$ cp evdev.lst /usr/share/X11/xkb/rules
$ cp evdev.xml /usr/share/X11/xkb/rules
```

You may have to prepend `sudo` or `gksu` to make this work.

### Restart
Restart the X server using `Ctrl+alt+Backspace`, or simply restart your machine for the changes to take effect.  
If anything went wrong, restore the original files from the backup you made earlier and restart again.


## Gnome
Gnome is known to be difficult with XKB, so it may require some fiddling with dconf to make it work. Normally, the new variant is picked up by Gnome and you can just use it like any other one in the control center. Sometimes, Gnome just doesn't want to play by the rules. In this case, just configure your input methods in dconf. Under `org.gnome.desktop.input-sources`, configure the `sources` and `current` (and optionally `xkb-options`) keys.

### sources
The value of the sources key is a list of tuples containing two strings: the first is `xkb` or `ibus`, the second the layout to be used, of the form `layout+variant`. Example:
```
('xkb','be+mac'),('xkb','be'),('xkb','fr')
```

### current
The (zero-based) index of the current input method. In the above example, if you want to use the `be+mac` layout, set this to `0`, or `1` for `be`, or `2` for `fr`.
