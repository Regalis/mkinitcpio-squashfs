# Project moved

This project has been moved. Project is now supported by **Regalis Technologies** company from Poland. New location: [RegalisTechnologies/mkinitcpio-squashfs](https://github.com/RegalisTechnologies/mkinitcpio-squashfs) 

mkinitcpio-squashfs
===================

This hook allows the user to mount SquashFS image as root.

Image can be stored on local (or remote - read about NBD) block device
or downloaded from remote location.

List of supported protocols:
  * HTTP
  * HTTPS
  * FTP

Kernel parameters:
------------------

* squashfs=\<image-source\>
* squashfs\_copy=\<image-copy\>

*\<image-source\>* can be remote or local location.

For remote location just use URL for example:

* squashfs=http://192.168.1.1/images/archlinux.squashfs

for local location use **DEVICE:PATH** syntax for example:

* squashfs=/dev/sda1:/images/archlinux.squashfs
* squashfs=LABEL=SquashFSImages:/images/archlinux.squashfs
* squashfs=UUID=3c1d5e55-(...):/images/archlinux.squashfs

It is also possible to type *AUTO* as *PATH*, then script will search for
**first file** which name ends with .sfs or .squashfs

*\<image-copy\>* can be one of {true, 1, 0, false} default is false

If *\<image-copy\>* is set to true or 1, then *\<image-source\>* will be copied
to RAM. This option is forced to true while you use remote location.

Example with squashfs\_copy:

* squashfs=/dev/sda1:/images/archlinux.squashfs squashfs\_copy=true

**NOTE**: After copying, you can remove device from your computer

mkinitcpio.conf
---------------

If you are going to use remote locations, add *net* (from mkinitcpio-nfs-utils)
before *squashfs* for example:

* HOOKS="base udev modconf keyboard **block net** squashfs filesystems"

It is also required to place *block* before squashfs if you will use
block devices as image source.


License
=======

Copyright (C) 2013 Patryk Jaworski \<regalis@regalis.com.pl\>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see http://www.gnu.org/licenses.
