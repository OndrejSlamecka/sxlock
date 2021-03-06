sxlock - simple X screen locker
===============================

Simple screen locker utility for X, fork of sflock, which is based on slock. Main difference is that
sxlock uses PAM authentication, so no suid is needed.


Features
--------

 - provides basic user feedback
 - uses PAM
 - sets DPMS timeout to 10 seconds, before exit restores original settings
 - basic RandR support (drawing centered on the primary output)


Requirements
------------

 - libX11 (Xlib headers)
 - libXext (X11 extensions library, for DPMS)
 - libXrandr (RandR support)
 - libXft
 - PAM


Installation
------------

Arch Linux users can install this package from the [AUR](https://aur.archlinux.org/packages/sxlock-git/).

For manual installation just install dependencies, checkout and make:

    git clone git://github.com/lahwaacz/sxlock.git
    cd ./sxlock
    make
    ./sxlock


Running sxlock
-------------

Simply invoking the sxlock command starts the display locker with default settings.

Custom settings:

    -f <font description>: modify the font.
    -p <password characters>: modify the characters displayed when the user enters his password. This can be a sequence of characters to create a fake password.
    -u <username>: a user name to be displayed at the lock screen.

Hooking into systemd events
---------------------------

When using [systemd](http://freedesktop.org/wiki/Software/systemd/), you can use the following service (create `/etc/systemd/system/sxlock.service`) to let the system lock your X session on hibernation or suspend:

```ini
[Unit]
Description=Lock X session using sxlock

[Service]
User=<username>
Environment=DISPLAY=:0
ExecStart=/usr/bin/sxlock

[Install]
WantedBy=sleep.target
```

However, this approach is useful only for single-user systems, because there is no way to know which user is currently logged in. Use [xss-lock](https://bitbucket.org/raymonad/xss-lock) as an alternative for multi-user systems.
