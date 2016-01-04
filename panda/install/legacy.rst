Legacy method
=============

First installation boot
-----------------------

First system loading will cause that the system partition will be expanded to the size of memory card. That process **cannot be interrupted**. You **need to wait** till the moment when one of LEDs will blink.

.. note::

    If you have display with HDMI input and keyboard or serial port in your PC, you are able to follow instructions which will be displayed on console (official method). If you do not have it, it is able to finish system installation as per this instruction.

* **Turn on** *PandaBoard*.
* **Wait** till the moment when on of LEDs will blink.
* **Turn off** *PandaBoard*.
* **Pull out** memory card from *PandaBoard* card reader.
* **Put** memory card in computer card reader.

Prepare system to configuration
-------------------------------

* **Mount** system partition (second partition).
* **Change** file which has network settings, which is located on system partition - path ``/etc/network/interfaces``.

::

    # interfaces(5) file used by ifup(8) and ifdown(8)
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
        address 192.168.2.50
        netmask 255.255.255.0
        gateway 192.168.2.1
        dns-nameservers 8.8.8.8

.. note::

    Applied configuration causes assigning address ``192.168.2.50`` in network ``192.168.2.0/24`` to the wired interface which is located on board. Additionally, default gateway is set with IP address ``192.168.2.1`` and DNS with IP ``8.8.8.8``.

.. warning::

    **Attentione!** That addressing schema is used in network in laboratory. In your network might be different. Please check it.

.. warning::

    Network ``192.168.2.0/24`` **eventually** is used on wireless interface. Configuration will be changed in next steps of this instruction, in step related to `updating network settings`_.

.. _updating network settings: #updatenetwork

* **Change** file which is located on system partition - path ``/etc/rc.local``.

.. code-block:: sh

    #!/bin/sh -e
    #
    # rc.local
    #
    # This script is executed at the end of each multiuser runlevel.
    # Make sure that the script will "exit 0" on success or any other
    # value on error.
    #
    # In order to enable or disable this script just change the execution
    # bits.
    #
    # By default this script does nothing.

    apt-get install -y openssh-server

    exit 0

.. note::

    That configuration causes installation of remote access server SSH when the system is booting. Remember that after first login you need to remove line starting with ``apt-get...`` from file ``/etc/rc.local``.

* **Change** file responsible for passwords, by removing characters ``x`` or ``*`` from fields responsible for password, which are in files ``/etc/passwd`` and ``/etc/shadow``.

.. code-block:: sh

    #-/etc/passwd
    root::0:0:root:/root:/bin/bash

    #-/etc/shadow
    root::15454:0:99999:7:::

.. note::

    That changes will remove password for ``root`` account. After first login please remember about setting password for administrator.

* **Add** your own public SSH key to file ``/root/.ssh/authorized_keys``

.. code-block:: sh

    ssh-rsa AAA... user@hostname

.. note::

    Your public SSH key is located in file ``~/.ssh/id_rsa.pub``. If you do not have this file it means that you do not have SSH key. To generate the private and public key, please execute command ``ssh-keygen``. That works on Linux only.

* **Unmount** system partition.
* **Pull out** card from reader.
* **Connect** board with network device, eg. switch, using network cable..
* **Put** card in reader in *PandaBoard*.
* **Turn on** *PandaBoard*.

Second configuration boot
-------------------------

* **Login** to the system using SSH ``ssh root@192.168.2.50``.
* **Set** password for ``root`` using command ``passwd root``.
* **Remove** line ``apt-get install -y openssh-server`` from file ``/etc/rc.local``.
* **Set** system name in file:

``/etc/hostname``

.. code-block:: sh

    panda.robonet

``/etc/hosts``

.. code-block:: sh

    127.0.0.1 localhost
    127.0.1.1 panda panda.robonet

.. warning::

    **Interrupt** board wizard configuration which is running on the console (available when serial port is used).

* **Execute** command ``fuser -k /var/cache/debconf/config.dat`` sevaral times.
* **Remove** package ``oem-config`` (using ``aptitude`` - ``aptitude purge oem-config``) and directory ``/var/lib/oem-config``.
* **Restart** system using command ``reboot``.

Updating software
-----------------

Updating system
~~~~~~~~~~~~~~~

* **Install** *screen* using ``aptitude install screen``.
* **Start** *screen* using ``screen``.

.. warning::

    It is available updating to *Ubuntu 14.04.1* LTS using command ``do-release-upgrade``. Due to issues with modules for devices *Ninedof* and *Roboclaw* it is **not recommended**. Following steps could skipped and you can jump to step related to `updating packages`_.

.. _updating packages: #updatepackages

.. note::

    Update process executed by command ``do-release-upgrade`` can take few minutes. Using *screen* prevents situation that command execution will be interrupted and allows detaching from console/session with keys ``[Ctrl]+[a]`` and ``[d]``.  Reconnecting can be done by executing command ``screen -r``.

.. warning::

    Please monitor updating process. During updating there will be several questions. When updating process will finish system need to be rebooted. Reboot need to be confirmed.

.. seealso::

    Packages which are used by *PandaBoard* are published in the repository http://ports.ubuntu.com/pool/main/l/linux-ti-omap4/.

After finished update by tool ``do-release-upgrade`` system does not support wireless network. You need **add** *omap* repository to repositories. After this, **update** packages list need to be done and following packages need to be installed:

.. code-block:: sh

    aptitude install -y software-properties-common
    add-apt-repository ppa:tiomap-dev/release
    aptitude update
    touch /boot/initrd.img-3.13.0-37-generic
    aptitude install linux-headers-omap linux-image-omap linux-omap

.. warning::

    Kernel installation requires files in directory ``/boot/``. When some files are missing, please create them using command ``touch``.

* **Execute** ``reboot``.

.. _updatepackages:

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

.. _updatenetwork:

* **Change** network settings: to file ``/etc/network/interfaces`` add settings related to wireless network:

::

    # interfaces(5) file used by ifup(8) and ifdown(8)
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
        wpa-psk  "PSK"

.. note::

    To have correctly working wireless network MAC address need to be setup manually.

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

* **Reboot** system.
* **Connect** to the system using IP address assigned by router. You can check it via administrative portal.

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

Post-configuration
------------------

* **Add** to ``/etc/modules`` line:
::

    ...
    i2c-dev


* **Update** ``/etc/init.d/cpufrequtils``:
::

    ...
    GOVERNOR="performance"
    ...

* **Be aware** about script ``/etc/init.d/ondemand``. It need to be disabled from runlevel by command ``update-rc.d -f ondemand remove``.
