Official method
===============

First installation boot
-----------------------

* **Start** application used for serial port communication, eg. ``miniterm`` or ``minicom``.

.. note::

    *PandaBoard* provides communication over serial port. Port baud speed is 115200bps.

* **Connect** *PandaBoard* to PC with serial port.
* **Turn on** *PandaBoard*.

First system loading will cause that the system partition will be expanded to the size of memory card. That process **cannot be interrupted**. You **need to wait** till the moment when one of LEDs will blink.

For the first time configuration wizard will be started. Instructions will be displayed on the console.

.. code-block:: sh

    (local) ➜ sudo miniterm.py -b 115200 -p /dev/ttyUSB3
    --- Miniterm on /dev/ttyUSB3: 115200,8,N,1 ---
    --- Quit: Ctrl+]  |  Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---

    U-Boot SPL 2011.12 (Apr 02 2012 - 18:13:04)
    Texas Instruments OMAP4460 ES1.1
    OMAP SD/MMC: 0
    reading u-boot.img
    reading u-boot.bin
    mkimage signature not found - ih_magic = ea000014
    Assuming u-boot.bin ..
    reading u-boot.bin


    U-Boot 2011.12 (Apr 02 2012 - 18:13:04)

    CPU  : OMAP4460 ES1.1
    Board: OMAP4 Panda
    I2C:   ready
    DRAM:  1 GiB
    WARNING: Caches not enabled
    MMC:   OMAP SD/MMC: 0
    Using default environment

    In:    serial
    Out:   serial
    Err:   serial
    Net:   No ethernet found.
    checking for preEnv.txt
    reading preEnv.txt

    ** Unable to read "preEnv.txt" from mmc 0:1 **
    Hit any key to stop autoboot:  0
    reading uEnv.txt

    ** Unable to read "uEnv.txt" from mmc 0:1 **
    reading boot.scr

    350 bytes read
    Loaded script from boot.scr
    Running bootscript from mmc0 ...
    ## Executing script at 82000000
    reading uImage

    4434784 bytes read
    reading uInitrd

    4314202 bytes read
    ## Booting kernel from Legacy Image at 80000000 ...
       Image Name:   Ubuntu Kernel
       Image Type:   ARM Linux Kernel Image (uncompressed)
       Data Size:    4434720 Bytes = 4.2 MiB
       Load Address: 80008000
       Entry Point:  80008000
       Verifying Checksum ... OK
    ## Loading init Ramdisk from Legacy Image at 81600000 ...
       Image Name:   Ubuntu Initrd
       Image Type:   ARM Linux RAMDisk Image (gzip compressed)
       Data Size:    4314138 Bytes = 4.1 MiB
       Load Address: 00000000
       Entry Point:  00000000
       Verifying Checksum ... OK
       Loading Kernel Image ... OK
    OK

    Starting kernel ...

    Uncompressing Linux... done, booting the kernel.
    Resizing root partition ...

    Disk /dev/mmcblk0: 3790 cylinders, 128 heads, 32 sectors/track
    Old situation:
    Units = sectors of 512 bytes, counting from 0

       Device Boot    Start       End   #sectors  Id  System
    /dev/mmcblk0p1   *        32    147455     147424   c  W95 FAT32 (LBA)
    /dev/mmcblk0p2        147456   3104767    2957312  83  Linux
    /dev/mmcblk0p3             0         -          0   0  Empty
    /dev/mmcblk0p4             0         -          0   0  Empty
    New situation:
    Units = sectors of 512 bytes, counting from 0

       Device Boot    Start       End   #sectors  Id  System
    /dev/mmcblk0p1   *        32    147455     147424   c  W95 FAT32 (LBA)
    /dev/mmcblk0p2        147456  15523839   15376384  83  Linux
    /dev/mmcblk0p3             0         -          0   0  Empty
    /dev/mmcblk0p4             0         -          0   0  Empty
    Successfully wrote the new partition table

    Re-reading the partition table ...

    If you created or changed a DOS partition, /dev/foo7, say, then use dd(1)
    to zero the first 512 bytes:  dd if=/dev/zero of=/dev/foo7 bs=512 count=1
    (See fdisk(8).)
    Resizing root filesystem. Please wait, this will take a moment ...
    Checking filesystem before resizing...
    Resizing, please wait...

For the first time system partition will be expanded to the size of memory card.

.. code-block:: sh

    Enabling serial console login
    Setting up fstab
    Setting up swap
    Enabling oem-config
    Writing flash-kernel configuration
    Creating bootloader configuration
    Rebooting into configuration session
    [   94.273376] Restarting system.

Second configuration boot
-------------------------

Configuration wizard will be started:

.. code-block:: sh

    U-Boot SPL 2011.12 (Apr 02 2012 - 18:13:04)
    Texas Instruments OMAP4460 ES1.1
    OMAP SD/MMC: 0
    reading u-boot.img
    reading u-boot.bin
    mkimage signature not found - ih_magic = ea000014
    Assuming u-boot.bin ..
    reading u-boot.bin


    U-Boot 2011.12 (Apr 02 2012 - 18:13:04)

    CPU  : OMAP4460 ES1.1
    Board: OMAP4 Panda
    I2C:   ready
    DRAM:  1 GiB
    WARNING: Caches not enabled
    MMC:   OMAP SD/MMC: 0
    Using default environment

    In:    serial
    Out:   serial
    Err:   serial
    Net:   No ethernet found.
    checking for preEnv.txt
    reading preEnv.txt

    ** Unable to read "preEnv.txt" from mmc 0:1 **
    Hit any key to stop autoboot:  0
    reading uEnv.txt

    ** Unable to read "uEnv.txt" from mmc 0:1 **
    reading boot.scr

    373 bytes read
    Loaded script from boot.scr
    Running bootscript from mmc0 ...
    ## Executing script at 82000000
    reading uImage

    4434784 bytes read
    reading uInitrd

    4314202 bytes read
    ## Booting kernel from Legacy Image at 80000000 ...
       Image Name:   Ubuntu Kernel
       Image Type:   ARM Linux Kernel Image (uncompressed)
       Data Size:    4434720 Bytes = 4.2 MiB
       Load Address: 80008000
       Entry Point:  80008000
       Verifying Checksum ... OK
    ## Loading init Ramdisk from Legacy Image at 81600000 ...
       Image Name:   Ubuntu Initrd
       Image Type:   ARM Linux RAMDisk Image (gzip compressed)
       Data Size:    4314138 Bytes = 4.1 MiB
       Load Address: 00000000
       Entry Point:  00000000
       Verifying Checksum ... OK
       Loading Kernel Image ... OK
    OK

    Starting kernel ...

    Uncompressing Linux... done, booting the kernel.
    fsck from util-linux 2.20.1
    /dev/mmcblk0p2: clean, 29269/961536 files, 1651666/7688192 blocks
     * Starting system logging daemon                                        [ OK ]
     * Starting load fallback graphics devices                               [ OK ]
     * Stopping load fallback graphics devices                               [ OK ]
    ...

After loading system wizard screen will be displayed.

First step is selecting language:

.. code-block:: sh

    System Configuration
      ┌──────────────────────────┤ Select a language ├──────────────────────────┐
      │ Choose the language to be used for the installation process. The        │
      │ selected language will also be the default language for the installed   │
      │ system.                                                                 │
      │                                                                         │
      │ Language:                                                               │
      │                                                                         │
      │               Bulgarian - Български                        ↑            │
      │               Catalan - Català                             ▒            │
      │               Chinese (Simplified) - 中文(简体)             ▮            │
      │               Chinese (Traditional) - 中文(繁體)            ▒            │
      │               Croatian - Hrvatski                          ▒            │
      │               Czech - Čeština                              ▒            │
      │               Danish - Dansk                               ▒            │
      │               Dutch - Nederlands                           ▒            │
      │               English - English                            ↓            │
      │                                                                         │
      │                                                                         │
      │                   <Ok>                       <Cancel>                   │
      │                                                                         │
      └─────────────────────────────────────────────────────────────────────────┘

Next step is selecting country:

.. code-block:: sh

    System Configuration
      ┌────────────────────────┤ Select your location ├─────────────────────────┐
      │ The selected location will be used to set your time zone and also for   │
      │ example to help select the system locale. Normally this should be the   │
      │ country where you live.                                                 │
      │                                                                         │
      │ This is a shortlist of locations based on the language you selected.    │
      │ Choose "other" if your location is not listed.                          │
      │                                                                         │
      │ Country, territory or area:                                             │
      │                                                                         │
      │                          Nigeria                ↑                       │
      │                          Philippines            ▒                       │
      │                          Singapore              ▒                       │
      │                          South Africa           ▮                       │
      │                          United Kingdom         ▒                       │
      │                          United States          ↓                       │
      │                                                                         │
      │                                                                         │
      │                   <Ok>                       <Cancel>                   │
      │                                                                         │
      └─────────────────────────────────────────────────────────────────────────┘

By selecting other next screen will display list of continents:

.. code-block:: sh

    System Configuration
      ┌────────────────────────┤ Select your location ├─────────────────────────┐
      │ The selected location will be used to set your time zone and also for   │
      │ example to help select the system locale. Normally this should be the   │
      │ country where you live.                                                 │
      │                                                                         │
      │ Select the continent or region to which your location belongs.          │
      │                                                                         │
      │ Continent or region:                                                    │
      │                                                                         │
      │                            Asia               ↑                         │
      │                            Atlantic Ocean     ▒                         │
      │                            Caribbean          ▒                         │
      │                            Central America    ▒                         │
      │                            Europe             ▮                         │
      │                            Indian Ocean       ▒                         │
      │                            North America      ↓                         │
      │                                                                         │
      │                                                                         │
      │                   <Ok>                       <Cancel>                   │
      │                                                                         │
      └─────────────────────────────────────────────────────────────────────────┘

After selecting continent next step will be again selecting country:

.. code-block:: sh

    System Configuration
      ┌─────────────────────────┤ Select your location ├─────────────────────────┐
      │ The selected location will be used to set your time zone and also for    │
      │ example to help select the system locale. Normally this should be the    │
      │ country where you live.                                                  │
      │                                                                          │
      │ Listed are locations for: Europe. Use the <Go Back> option to select a   │
      │ different continent or region if your location is not listed.            │
      │                                                                          │
      │ Country, territory or area:                                              │
      │                                                                          │
      │                     Poland                           ↑                   │
      │                     Portugal                         ▒                   │
      │                     Romania                          ▒                   │
      │                     Russian Federation               ▮                   │
      │                     San Marino                       ▒                   │
      │                     Serbia                           ↓                   │
      │                                                                          │
      │                                                                          │
      │                   <Ok>                       <Cancel>                    │
      │                                                                          │
      └──────────────────────────────────────────────────────────────────────────┘

Next step is selecting locales settings:

.. code-block:: sh

    System Configuration
      ┌──────────────────────────┤ Configure locales ├───────────────────────────┐
      │ There is no locale defined for the combination of language and country   │
      │ you have selected. You can now select your preference from the locales   │
      │ available for the selected language. The locale that will be used is     │
      │ listed in the second column.                                             │
      │                                                                          │
      │ Country to base default locale settings on:                              │
      │                                                                          │
      │                      Ireland - en_IE.UTF-8           ↑                   │
      │                      New Zealand - en_NZ.UTF-8       ▒                   │
      │                      Nigeria - en_NG                 ▒                   │
      │                      Philippines - en_PH.UTF-8       ▒                   │
      │                      Singapore - en_SG.UTF-8         ▒                   │
      │                      South Africa - en_ZA.UTF-8      ▮                   │
      │                      United Kingdom - en_GB.UTF-8    ▒                   │
      │                      United States - en_US.UTF-8     ↓                   │
      │                                                                          │
      │                                                                          │
      │                   <Ok>                       <Cancel>                    │
      │                                                                          │
      └──────────────────────────────────────────────────────────────────────────┘

Next step is selecting time zone used in selected location:

.. code-block:: sh

  System Configuration
    ┌───────────────────────────┤ Where are you? ├────────────────────────────┐
    │                                                                         │
    │ Based on your country, your time zone is Europe/Warsaw.                 │
    │                                                                         │
    │ If this is not correct, you may select from a full list of time zones   │
    │ instead.                                                                │
    │                                                                         │
    │ Is this time zone correct?                                              │
    │                                                                         │
    │                    <Yes>                       <No>                     │
    │                                                                         │
    └─────────────────────────────────────────────────────────────────────────┘

Next step is selecting time zone of hardware clock:

.. code-block:: sh

    System Configuration
     ┌────────────────────────────┤ Where are you? ├─────────────────────────────┐
     │                                                                           │
     │ System clocks are generally set to Coordinated Universal Time (UTC). The  │
     │ operating system uses your time zone to convert system time into local    │
     │ time. This is recommended unless you also use another operating system    │
     │ that expects the clock to be set to local time.                           │
     │                                                                           │
     │ Is the system clock set to UTC?                                           │
     │                                                                           │
     │                    <Yes>                       <No>                       │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

Next step is setting full name of user:

.. code-block:: sh

    System Configuration
     ┌─────────────────────────────┤ Who are you? ├──────────────────────────────┐
     │ A user account will be created for you to use instead of the root         │
     │ account for non-administrative activities.                                │
     │                                                                           │
     │ Please enter the real name of this user. This information will be used    │
     │ for instance as default origin for emails sent by this user as well as    │
     │ any program which displays or uses the user's real name. Your full name   │
     │ is a reasonable choice.                                                   │
     │                                                                           │
     │ Full name for the new user:                                               │
     │                                                                           │
     │ _________________________________________________________________________ │
     │                                                                           │
     │                    <Ok>                        <Cancel>                   │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

Next step is setting name of user:

.. code-block:: sh

    System Configuration
     ┌─────────────────────────────┤ Who are you? ├──────────────────────────────┐
     │ Select a username for the new account. Your first name is a reasonable    │
     │ choice. The username should start with a lower-case letter, which can be  │
     │ followed by any combination of numbers and more lower-case letters.       │
     │                                                                           │
     │ Username for your account:                                                │
     │                                                                           │
     │ robolab__________________________________________________________________ │
     │                                                                           │
     │                    <Ok>                        <Cancel>                   │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

Next step is setting password for user:

.. code-block:: sh

    System Configuration
          ┌─────────────────────────┤ Who are you? ├─────────────────────────┐
          │ A good password will contain a mixture of letters, numbers and   │
          │ punctuation and should be changed at regular intervals.          │
          │                                                                  │
          │ Choose a password for the new user:                              │
          │                                                                  │
          │ ________________________________________________________________ │
          │                                                                  │
          │                 <Ok>                     <Cancel>                │
          │                                                                  │
          └──────────────────────────────────────────────────────────────────┘

Next step is repeating password.

Next step is setting default network interface:

.. code-block:: sh

    System Configuration
     ┌─────────────────────────┤ Network configuration ├─────────────────────────┐
     │ Your system has multiple network interfaces. Choose the one to use as     │
     │ the primary network interface during the installation. If possible, the   │
     │ first connected network interface found has been selected.                │
     │                                                                           │
     │ Primary network interface:                                                │
     │                                                                           │
     │                    eth0: Ethernet                                         │
     │                    wlan0: Wireless ethernet (802.11x)                     │
     │                                                                           │
     │                                                                           │
     │                    <Ok>                        <Cancel>                   │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

``eth0`` should be selected. After this, network testing will be done. There is no need to finish test with success:

.. code-block:: sh

    System Configuration
     ┌─────────────────────────┤ Network configuration ├─────────────────────────┐
     │                                                                           │
     │ Network autoconfiguration failed                                          │
     │                                                                           │
     │ Your network is probably not using the DHCP protocol. Alternatively, the  │
     │ DHCP server may be slow or some network hardware is not working           │
     │ properly.                                                                 │
     │                                                                           │
     │                                  <Ok>                                     │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

If this test was not finished with success, address need to be set manually:

.. code-block:: sh

    System Configuration
     ┌─────────────────────────┤ Network configuration ├─────────────────────────┐
     │ From here you can choose to retry DHCP network autoconfiguration (which   │
     │ may succeed if your DHCP server takes a long time to respond) or to       │
     │ configure the network manually. Some DHCP servers require a DHCP          │
     │ hostname to be sent by the client, so you can also choose to retry DHCP   │
     │ network autoconfiguration with a hostname that you provide.               │
     │                                                                           │
     │ Network configuration method:                                             │
     │                                                                           │
     │           Retry network autoconfiguration                                 │
     │           Retry network autoconfiguration with a DHCP hostname            │
     │           Configure network manually                                      │
     │                                                                           │
     │           Do not configure the network at this time                       │
     │                                                                           │
     │                                                                           │
     │                    <Ok>                        <Cancel>                   │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

.. code-block:: sh

    System Configuration
      ┌────────────────────────┤ Network configuration ├─────────────────────────┐
      │ The IP address is unique to your computer and is either:                 │
      │                                                                          │
      │ * Four numbers separated by periods; or                                  │
      │                                                                          │
      │ * Blocks of hexadecimal characters separated by colons (IPv6).           │
      │                                                                          │
      │ You can also optionally specify a CIDR netmask.                          │
      │                                                                          │
      │ If you don't know what to use here, consult your network administrator.  │
      │                                                                          │
      │ IP address:                                                              │
      │                                                                          │
      │ 192.168.1.50____________________________________________________________ │
      │                                                                          │
      │                   <Ok>                       <Cancel>                    │
      │                                                                          │
      └──────────────────────────────────────────────────────────────────────────┘

.. code-block:: sh

    System Configuration
       ┌───────────────────────┤ Network configuration ├───────────────────────┐
       │ The netmask is used to determine which machines are local to your     │
       │ network.  Consult your network administrator if you do not know the   │
       │ value.  The netmask should be entered as four numbers separated by    │
       │ periods.                                                              │
       │                                                                       │
       │ Netmask:                                                              │
       │                                                                       │
       │ 255.255.255.0________________________________________________________ │
       │                                                                       │
       │                  <Ok>                      <Cancel>                   │
       │                                                                       │
       └───────────────────────────────────────────────────────────────────────┘

.. code-block:: sh

    System Configuration
      ┌────────────────────────┤ Network configuration ├─────────────────────────┐
      │ The gateway is an IP address (four numbers separated by periods) that    │
      │ indicates the gateway router, also known as the default router.  All     │
      │ traffic that goes outside your LAN (for instance, to the Internet) is    │
      │ sent through this router.  In rare circumstances, you may have no        │
      │ router; in that case, you can leave this blank.  If you don't know the   │
      │ proper answer to this question, consult your network administrator.      │
      │                                                                          │
      │ Gateway:                                                                 │
      │                                                                          │
      │ 192.168.1.1_____________________________________________________________ │
      │                                                                          │
      │                   <Ok>                       <Cancel>                    │
      │                                                                          │
      └──────────────────────────────────────────────────────────────────────────┘

.. code-block:: sh

    System Configuration
     ┌─────────────────────────┤ Network configuration ├─────────────────────────┐
     │ The name servers are used to look up host names on the network. Please    │
     │ enter the IP addresses (not host names) of up to 3 name servers,          │
     │ separated by spaces. Do not use commas. The first name server in the      │
     │ list will be the first to be queried. If you don't want to use any name   │
     │ server, just leave this field blank.                                      │
     │                                                                           │
     │ Name server addresses:                                                    │
     │                                                                           │
     │ 192.168.1.1______________________________________________________________ │
     │                                                                           │
     │                    <Ok>                        <Cancel>                   │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

.. warning::

    Above configuration causes assigning address ``192.168.2.50`` in network ``192.168.2.0/24`` to the wired interface which is located on board. Additionally, default gateway is set with IP address ``192.168.2.1`` and DNS with IP ``8.8.8.8``.

Next step is setting system name and domain:

.. code-block:: sh

    System Configuration
     ┌─────────────────────────┤ Network configuration ├─────────────────────────┐
     │ Please enter the hostname for this system.                                │
     │                                                                           │
     │ The hostname is a single word that identifies your system to the          │
     │ network. If you don't know what your hostname should be, consult your     │
     │ network administrator. If you are setting up your own home network, you   │
     │ can make something up here.                                               │
     │                                                                           │
     │ Hostname:                                                                 │
     │                                                                           │
     │ _________________________________________________________________________ │
     │                                                                           │
     │                    <Ok>                        <Cancel>                   │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

.. code-block:: sh

    System Configuration
     ┌─────────────────────────┤ Network configuration ├─────────────────────────┐
     │ The domain name is the part of your Internet address to the right of      │
     │ your host name.  It is often something that ends in .com, .net, .edu, or  │
     │ .org. If you are setting up a home network, you can make something up,    │
     │ but make sure you use the same domain name on all your computers.         │
     │                                                                           │
     │ Domain name:                                                              │
     │                                                                           │
     │ _________________________________________________________________________ │
     │                                                                           │
     │                    <Ok>                        <Cancel>                   │
     │                                                                           │
     └───────────────────────────────────────────────────────────────────────────┘

Next step is selecting basic system functions:

.. code-block:: sh

    System Configuration
        ┌───────────────────────┤ Software selection ├────────────────────────┐
        │ You can choose to install one or more of the following predefined   │
        │ collections of software.                                            │
        │                                                                     │
        │ Choose software to install:                                         │
        │                                                                     │
        │    [ ] Basic Ubuntu server                                          │
        │    [*] OpenSSH server                                               │
        │    [ ] DNS server                                                   │
        │    [ ] LAMP server                                                  │
        │    [ ] Mail server                                                  │
        │    [ ] PostgreSQL database                                          │
        │    [ ] Print server                                                 │
        │    [ ] Samba file server                                            │
        │    [ ] Tomcat Java server                                           │
        │    [ ] Virtual Machine host                                         │
        │                                                                     │
        │                                                                     │
        │                  <Ok>                      <Cancel>                 │
        │                                                                     │
        └─────────────────────────────────────────────────────────────────────┘

``OpenSSH server`` need to be selected. After this, SSH server will be installed, additional parameters will be set and unused packages will be removed. After this, there will be login prompt displayed:

.. code-block:: sh

    Ubuntu 12.04 LTS hostname ttyO2

    hostname login: username
    Password:
    Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-1412-omap4 armv7l)

     * Documentation:  https://help.ubuntu.com/

    The programs included with the Ubuntu system are free software;
    the exact distribution terms for each program are described in the
    individual files in /usr/share/doc/*/copyright.

    Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
    applicable law.

    username@hostname:~$

Updating software
---------------------------

Cleaning packages
~~~~~~~~~~~~~~~~~

Unused packages need to be removed. To do this following command can be used ``sudo aptitude install``:

.. code-block:: sh

    username@hostname:~$ sudo aptitude install
    The following packages will be REMOVED:
      apt-clone{u} archdetect-deb{u} bc{u} bogl-bterm{u} btrfs-tools{u}
      dmraid{u} dpkg-repack{u} kpartx{u} kpartx-boot{u} libdebconfclient0{u}
      libdebian-installer4{u} libdmraid1.0.0.rc16{u} libicu48{u} os-prober{u}
      python-pyicu{u} rdate{u} realpath{u} reiserfsprogs{u}
    0 packages upgraded, 0 newly installed, 18 to remove and 0 not upgraded.
    Need to get 0 B of archives. After unpacking 24.6 MB will be freed.
    Do you want to continue? [Y/n/?] y

    (Reading database ... 24784 files and directories currently installed.)
    Removing apt-clone ...
    Removing archdetect-deb ...
    Removing bc ...
    Removing bogl-bterm ...
    Removing btrfs-tools ...
    Removing dmraid ...
    update-initramfs: deferring update (trigger activated)
    Removing dpkg-repack ...
    Removing kpartx-boot ...
    update-initramfs: deferring update (trigger activated)
    Removing kpartx ...
    Removing libdebconfclient0 ...
    Removing libdebian-installer4 ...
    Removing libdmraid1.0.0.rc16 ...
    Removing python-pyicu ...
    Removing libicu48 ...
    Removing os-prober ...
    Removing rdate ...
    Removing realpath ...
    Removing reiserfsprogs ...
    Processing triggers for man-db ...
    Processing triggers for install-info ...
    Processing triggers for initramfs-tools ...
    update-initramfs: Generating /boot/initrd.img-3.2.0-1412-omap4
    Using u-boot partition: /dev/mmcblk0p1
    Creating backups of boot files ... done.
    Generating kernel u-boot image... done.
    Generating Initramfs u-boot image... done.
    Generating u-boot configuration from /boot/boot.script... done.
    Processing triggers for libc-bin ...
    ldconfig deferred processing now taking place

Wireless card installation
~~~~~~~~~~~~~~~~~~~~~~~~~~

To use wireless card you need to install package ``wpasupplicant``:

.. code-block:: sh

    username@hostname:~$ sudo aptitude install wpasupplicant
    The following NEW packages will be installed:
      libpcsclite1{a} wpasupplicant
    0 packages upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
    Need to get 0 B/432 kB of archives. After unpacking 950 kB will be used.
    Do you want to continue? [Y/n/?] y

    Selecting previously unselected package libpcsclite1.
    (Reading database ... 24571 files and directories currently installed.)
    Unpacking libpcsclite1 (from .../libpcsclite1_1.7.4-2ubuntu2_armhf.deb) ...
    Selecting previously unselected package wpasupplicant.
    Unpacking wpasupplicant (from .../wpasupplicant_0.7.3-6ubuntu2_armhf.deb) ...
    Processing triggers for man-db ...
    Setting up libpcsclite1 (1.7.4-2ubuntu2) ...
    Setting up wpasupplicant (0.7.3-6ubuntu2) ...
    Processing triggers for libc-bin ...
    ldconfig deferred processing now taking place

After this, please update file ``/etc/network/interfaces``:

.. code-block:: sh

    sudo nano /etc/network/interfaces

    # This file describes the network interfaces available on your system
    # and how to activate them. For more information, see interfaces(5).

    # The loopback network interface
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
        address 192.168.1.50
        netmask 255.255.255.0

    auto wlan0
    iface wlan0 inet dhcp
        pre-up  ifconfig wlan0 hw ether de:ad:be:ef:00:10
        wpa-ssid "SSID"
        wpa-psk "PSK"

After saving changes, execute commands ``sudo ifconfig eth0 down`` and ``sudo ifup wlan0``. After this, please check network connectivity:

.. note::

    To have correctly working wireless network it is required to have MAC address manually set.

.. warning::

    Be aware that network addressing settings have been changed in last step due to fact that the same network cannot be used on both interfaces.

.. note::

    Above configuration is used in wireless network *robolab* which is in laboratory. Current preshared key for wireless network is published in laboratory. IP addresses are connected with MAC addresses. In laboratory used MAC prefix is ``de:ad:be:ef:00:**``. Last two characters decide which IP address will be assigned. Following scheme is used:

    ::

        de:ad:be:ef:00:00 - 192.168.2.200
        de:ad:be:ef:00:01 - 192.168.2.201
        ...
        de:ad:be:ef:00:09 - 192.168.2.209
        de:ad:be:ef:00:10 - 192.168.2.210

Updating system
~~~~~~~~~~~~~~~

.. warning::

    It is available updating to *Ubuntu 14.04.1* LTS using command ``do-release-upgrade``. Due to issues with modules for devices *Ninedof* and *Roboclaw* it is **not recommended**. Following steps could skipped and you can jump to step related to `updating packages`_.

.. _updating packages: #updatepackages

.. note::

    Update process executed by command ``do-release-upgrade`` can take few minutes. Using *screen* prevents situation that command execution will be interrupted and allows detaching from console/session with keys ``[Ctrl]+[a]`` and ``[d]``.  Reconnecting can be done by executing command ``screen -r``.

.. warning::

    Please monitor updating process. During updating there will be several questions. When updating process will finish system need to be rebooted. Reboot need to be confirmed.

.. seealso::

    Packages which are used by *PandaBoard* are published in the repository http://ports.ubuntu.com/pool/main/l/linux-ti-omap4/.

After update done by tool ``do-release-upgrade`` system does not support wireless network. You need **add** *omap* repository to repositories. After this, **update** packages list need to be done and following packages need to be installed:

.. code-block:: sh

    aptitude install -y software-properties-common
    add-apt-repository ppa:tiomap-dev/release
    aptitude update
    touch /boot/initrd.img-3.13.0-37-generic
    aptitude install linux-headers-omap linux-image-omap linux-omap

.. warning::

    Kernel installation requires files in directory ``/boot/``. When some files are missing, please create them using command ``touch``.

* **Execute** ``reboot``.

Updating packages
~~~~~~~~~~~~~~~~~

Recommended is to **turn off** installing recommended packages in *aptitude*:

* Start ``aptitude``
* Use keys ``[Ctrl]+[t]``
* Go to menu ``Options`` → ``Preferences``
* Disable option ``Install recommended packages automatically``
* Close *aptitude* using keys ``[Ctrl]+[q]``

* **Perform** update i **install** additional packages:

.. code-block:: sh

    aptitude update
    touch /boot/initrd.img-3.2.0-1455-omap4
    aptitude full-upgrade
    aptitude install -y
    aptitude install -y wpasupplicant wireless-crda wireless-regdb
    aptitude install -y htop psmisc mc unzip bash-completion cpufrequtils ntp
    aptitude install -y byobu tmux

.. warning::

    Kernel installation requires files in directory ``/boot/``. When some files are missing, please create them using command ``touch``.

* **Add** to file ``/etc/rc.local`` line ``iw reg set PL``.
* **Shutdown** system using command ``sudo poweroff``.

Updating bootloader
~~~~~~~~~~~~~~~~~~~

To have card combatible with board in version **B3**, you need download latest bootloader version *u-boot* and manually compile it as per following instruction. To execute following commands additional software need to be installed:

* make
* g++
* gcc
* u-boot-tools
* g++-arm-linux-gnueabihf
* gcc-arm-linux-gnueabihf
* binutils-arm-linux-gnueabihf

Command to execute: ``apt-get install make g++ gcc u-boot-tools g++-arm-linux-gnueabihf gcc-arm-linux-gnueabihf binutils-arm-linux-gnueabihf``.

For some distributions version need to be changed. For Debian, current ``testing`` version has listed packages.

.. code-block:: sh

    $ wget ftp://ftp.denx.de/pub/u-boot/u-boot-latest.tar.bz2
      [..]
    $ tar xf u-boot-latest.tar.bz2
    $ cd u-boot-*
    $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- omap4_panda_config
      HOSTCC  scripts/basic/fixdep
      HOSTCC  scripts/kconfig/conf.o
      SHIPPED scripts/kconfig/zconf.tab.c
      SHIPPED scripts/kconfig/zconf.lex.c
      SHIPPED scripts/kconfig/zconf.hash.c
      HOSTCC  scripts/kconfig/zconf.tab.o
      HOSTLD  scripts/kconfig/conf
    #
    # configuration written to .config
    #
    $ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-
      [..]
    $ cat <<EOF > boot.script
    fatload mmc 0:1 0x80000000 uImage
    setenv bootargs rw vram=32M fixrtc mem=1G@0x80000000 root=/dev/mmcblk0p2 console=ttyO2,115200n8 rootwait
    bootm 0x80000000
    EOF
    $ mkimage -A arm -T script -C none -n "Boot Image" -d boot.script boot.scr
      Image Name:   Boot Image
      Created:      Fri Nov 20 17:48:09 2015
      Image Type:   ARM Linux Script (uncompressed)
      Data Size:    164 Bytes = 0.16 kB = 0.00 MB
      Load Address: 00000000
      Entry Point:  00000000
      Contents:
        Image 0: 156 Bytes = 0.15 kB = 0.00 MB
    $ mkimage -A arm -T script -C none -n "Boot Image" -d boot.script boot.scr

As a result of these commands, following files will be generated and should be copied on first partition of memory card:

* ``boot.scr``
* ``boot.script``
* ``MLO``
* ``u-boot.bin``
* ``u-boot.img``

After copying that files, card can be used on both *PandaBoard* types **B2** and **B3**.

Post-konfiguracja
-----------------

* **Dodaj** do ``/etc/modules`` wpis:
::

    ...
    i2c-dev


* **Zmień** ``/etc/init.d/cpufrequtils``:
::

    ...
    GOVERNOR="performance"
    ...

* **Be aware** about script ``/etc/init.d/ondemand``. It need to be disabled from runlevel by command ``update-rc.d -f ondemand remove``.
