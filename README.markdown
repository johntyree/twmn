twmn
====
A notification system for tiling window managers. `twmn` is two things:

`twmnc`: command line tool to send notifications to `twmnd`. You can also use `notify-send` for a similar purpose, but `twmnc` is more powerful. See `twmnc --help` for more information.

`twmnd`: daemon listening to notification requests and showing them one after another. Configure it at `~/.config/twmn/twmn.conf`. The file is generated the first time `twmnd` is launched.

Notifications are shown in a one-line bar called the notification slide. They can be navigated through and activated with shortcuts.

See `twmn.conf` for more information.


About twmn.conf
---------------
<pre>
[gui]
; Screen number to display notifications on when using a multi-head desktop.
screen=  ; 0 indexed screen number

; WARNING: Deprecated by "screen"
; Absolute position from the top-left corner of the slide. You may need it for a multi-screen setup.
; You still have to set position in order to choose the slide animation. If empty, twmnd will try
; to figure out where to display the slide according to your desktop size and the slide position.
absolute_position=  ; Supported format: WxH. Width and Height being integers.

; Background color.
background_color=black  ; RBG hex and keywords (eg. lightgray) are supported.

; An icon for the layout. Useful only for a layout file.
icon=  ; Path to image file. Optional.

; Font family.
font=Sans

; Font size.
font_size=13  ; In pixel.

; Text color.
foreground_color=white  ; RBG hex and keywords (eg. lightgray) are supported.

; Height of the slide bar. Useful to match your tiling window manager's bar.
height=18  ; In pixel.

; Position of the notification slide.
position=top_right  ; Accepted values: top_right (tr), top_left (tl), bottom_right (br),
                    ; bottom_left (bl), top_center (tc), bottom_center (bc), center (c).

; The animation to use when the slide appear
in_animation=38 ; see http://qt-project.org/doc/qt-4.8/qeasingcurve.html#Type-enum for types

; The in animation's duration
in_animation_duration=1000 ; in milliseconds

; The animation to use whe the slide is closing
out_animation=13

; The out animation's duration
out_animation_duration=1000

; Enable or disable notification bounce when changing notification
bounce=true  ; true or false

[icons]
; An icon. You can add as many as you want.
NAME=  ; Path to image file. NAME being the icon's custom name.


[main]
; Program/command to be executed on notification activation.
activate_command=  ; Path to command.

; Time each notification remains visible.
duration=3000  ; In millisecond.

; Enable or disable shortcuts.
enable_shortcuts=true  ; true or false.

; UDP port used for notifications.
port=9797

; Program/command to play sound with.
sound_command=  ;  Path to command. Leave empty for no sound.


[shortcuts]
; Modifiers shortcuts.
modifiers=Alt+  ; Up to three modifiers. Use with the following shortcuts.

; Shows the previous notification. Mouse wheel up does it too.
previous=K

; Shows the next notification. If a modification is manually shown it will not be displayed again
; when twmnd process the notification stack. Mouse wheel up does it too.
next=J

; Activates the notification. Runs the command defined at activate_command.
; Mouse left click activates it too.
activate=Return

; Hides all notifications. To hide the current notification, use the "next" key
; instead. Mouse right click has the same effect.
hide=X
</pre>


Installation
------------

For [Arch Linux](http://www.archlinux.org/) users, `twmn` is [on the AUR](https://aur.archlinux.org/packages.php?ID=51596).

Otherwise you can install `twmnd` and `twmnc` manually:

1. install `boost`, `qt` and `dbus` if they weren't before
2. `git clone https://github.com/sboli/twmn.git` to get `twmn`
3. `cd twmn/`
4. `qmake` to generate a Makefile
5. `make` to compile
6. `sudo make install` to install `twmnd` and `twmnc` in `/usr/local/bin`. Make sure this folder is in your `$PATH` environment variable. (`export PATH=$PATH:/usr/local/bin`)
7. for `twmnd` to be always running, add it to your `.xinitrc`, `rc.conf` or else

The `storage_notifier` example requires `dbus-python` to be installed. The `mpd_notifier` example requires `python-mpd` to be installed and running.
