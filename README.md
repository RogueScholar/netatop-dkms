# netatop-dkms

## What's here

This repository contains the files needed to package and install the netatop kernel module on Debian-based systems, creating a .deb package which can be managed with `apt` or `dpkg`. It uses the dkms system to automatically build and load the module for all Linux kernels installed on the system via the package manager.

![networkmod][5]

More information about dkms and how it works can be found on its [official website][3].

## What is `netatop`

netatop is a module for Linux kernel 4.13 and up that can be loaded to gather statistics about the TCP and UDP packets that have been transmitted/received per process and per thread accessible through the application, `atop`. As soon as atop discovers that this module is active, it shows the columns SNET and RNET in the generic screen for the number of transmitted and received packets per process. When the 'n' key is pressed, it shows detailed counters about the number packets transmitted/received via TCP and UDP, the average sizes of these packets, and the total bandwidth consumed for input and output per process/thread.

![netatop-diagram][4]

A tarball of the  complete source code for the module and associated userspace daemon is available [here][2].

The module uses the netfilter interface offered by the kernel to gather these statistics. It is called for the network packets that pass the IP layer. For every packet, netatop tries to identify the process and thread involved. However, this is only possible from the moment that at least one packet has been transmitted for each connection (TCP) or port (UDP) within the context of the concerning process/thread. The filesystem location /proc/netatop offers direct access to the raw counters of identified and unidentified packets.

More information can be found on the [atop website][1].

[1]: https://www.atoptool.nl/netatop.php
[2]: https://www.atoptool.nl/download/netatop-2.0.tar.gz
[3]: https://github.com/dell/dkms
[4]: https://user-images.githubusercontent.com/15098724/60111885-a20e3380-9723-11e9-8dcc-5a18dd0490fb.gif
[5]: https://user-images.githubusercontent.com/15098724/60112371-86575d00-9724-11e9-8e7e-aaf735acebd3.png

