Pierwsze uruchomienie instalacyjne
----------------------------------

* **Uruchom** aplikację do pracy z portem szeregowym, np. ``miniterm`` lub ``minicom``.

.. note::

    *PandaBoard* udostępnia port komunikacji szeregowej. Port pracuje z szybkością 115200bps.

* **Podłącz** *PandaBoard* do komputera posiadającego port komunikacji szeregowej.
* **Uruchom** płytkę *PandaBoard*.

Pierwsze ładowanie systemu spowoduje, że partycja z systemem rozszerzy się do wielkości karty. **Nie należy przerywać** uruchamiania systemu. **Należy czekać** do momentu, gdy jedna z diod na płytce będzie mrugała cyklicznie.

W trakcie pierwszego uruchamiania, w oknie aplikacji użytej do komunikacji z płytką, pojawiać się będą komunikaty o instalacji.

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

W trakcie pierwszego uruchomienia następuje rozszerzenie partycji systemowej do rozmiarów użytej karty.

.. code-block:: sh

    Enabling serial console login
    Setting up fstab
    Setting up swap
    Enabling oem-config
    Writing flash-kernel configuration
    Creating bootloader configuration
    Rebooting into configuration session
    [   94.273376] Restarting system.

Drugie uruchomienie konfiguracyjne
----------------------------------

Po pierwszym uruchomieniu, następuje uruchomienie systemu.

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

Po załadowaniu systemu, pojawia się kreator konfiguracji systemu.

Pierwszym krokiem jest wybranie języka:

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

Kolejnym krokiem jest wybranie kraju:

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

Wybierając ``other``, kolejnym krokiem jest wybranie kontynentu:

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

Wybierając ``Europe``, kolejnym krokiem jest ponowne wybranie kraju:

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

Kolejnym krokiem jest wybranie ustawień lokalizacji:

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

Kolejnym krokiem jest wybranie strefy czasowej:

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

Kolejnym krokiem jest ustawienie strefy czasowej zegara płytki:

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

Kolejnym krokiem jest ustawienie pełnej nazwy użytkownika:

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


Kolejnym krokiem jest ustawienie nazwy użytkownika:

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

Kolejnym krokiem jest ustawienie hasła dla nowego użytkownika:

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

Następnym krokiem jego powtórzenie.

Kolejnym krokiem jest ustawienie domyślnego interfejsu sieciowego:

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

Należy wybrać ``eth0``. Po tym nastąpi testowanie łącza kablowego. Nie jest wymagane, by ono się zakończyło sukcesem:

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

Jeśli nie zakończyło się ono sukcesem, to należy manualnie ustawić adres sieciowy:

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

    Powyższa konfiguracja powoduje przypisanie adresu ``192.168.1.50`` w sieci ``192.168.1.0/24`` do interfejsu sieci przewodowej znajdującego się na płytce. Dodatkowo, ustawiona jest brama domyślna o adresie ``192.168.1.1`` oraz serwer nazw DNS ``192.168.1.1``. W twoim przypadku może być ona inna. Proszę, zwróć uwagę na adresację Twojej sieci.

Kolejnym krokiem jest ustawienie nazwy systemu oraz domeny:

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

Kolejnym krokiem jest wybranie podstawowych funkcji systemu:

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

Należy wybrać ``OpenSSH server``. Nastąpi instalacja serwera SSH, ustawienie dodatkowych parametrów oraz usunięcie zbędnych pakietów. Po zakończonym procesie, wyświetli się prośba o podanie nazwy użytkownika i hasło:

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

Aktualizacja oprogramowania
---------------------------

Czyszczenie pozostałych pakietów
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Po pierwszym uruchomieniu, należy wyczyścić pozostałe po instalacji pakiety poleceniem ``sudo aptitude install``:

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

Instalacja sieci bezprzewodowej
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Do obsługi sieci bezprzewodowej należy zainstalować pakiet ``wpasupplicant``:

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

Po instalacji pakietu ``wpasupplicant``, należy zmienić plik ``/etc/network/interfaces``:

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

Po zapisaniu zmian, wywołać polecenia ``sudo ifconfig eth0 down`` i ``sudo ifup wlan0``. Następnie sprawdzić połączenie z siecią.

Aktualizacja systemu
~~~~~~~~~~~~~~~~~~~~

.. warning::

    Możliwe jest wykonanie aktualizacji do *Ubuntu 14.04.1* LTS przy pomocy polecenia ``do-release-upgrade``. Ze względu na problemy w obsłudze sterowników dla urządzeń *Ninedof* oraz *Roboclaw* jest to **niezalecane**. Można pominąć poniższe kroki do kroku aktualizacji_ pakietów.

.. note::

    Proces aktualizacji przy pomocy ``do-release-upgrade`` może trwać kilka minut. Z wykorzystaniem screen możliwe jest odłączenie się od konsoli poprzez kombinacje klawiszy ``[Ctrl]+[a]`` i ``[d]``. Ponownie podłączenie następuje poprzez wywołanie polecenia ``screen -r``.

.. warning::

    Proszę monitorować stan aktualizacji. W trakcie aktualizacji pojawiać się będą pytania do akceptacji lub nie. Po zakończeniu procesu aktualizacji system zostanie uruchomiony ponownie, co wymaga potwierdzenia.

.. seealso::

    Miejscem, gdzie znajdują się pakiety używane na PandaBoard jest repozytorium http://ports.ubuntu.com/ w `linux-ti-omap`_.

Po wykonaniu aktualizacji przy pomocy ``do-release-upgrade``, system nie wspiera WiFi. Należy **dodać** do repozytoriów *apt* repozytorium *omap*. Następnie wykonać **aktualizację** listy pakietów i **instalację** następujących pakietów:

.. code-block:: sh

    aptitude install -y software-properties-common
    add-apt-repository ppa:tiomap-dev/release
    aptitude update
    touch /boot/initrd.img-3.13.0-37-generic
    aptitude install linux-headers-omap linux-image-omap linux-omap

.. warning::

    Instalacja jądra systemu wymaga obecności plików w katalogu ``/boot/``. W razie ich braku, wystarczy stworzyć brakujący plik przy pomocy polecenia ``touch``.

* **Wykonaj** ``reboot``.

.. _aktualizacji:

Aktualizacja pakietów
~~~~~~~~~~~~~~~~~~~~~

Polecam **wyłączyć** opcję instalowania polecanych pakietów w *aptitude*:

* Uruchomić ``aptitude``
* Skrót klawiszowy ``[Ctrl]+[t]``
* Wybór menu ``Options`` → ``Preferences``
* Odznaczyć ``Install recommended packages automatically``
* Wyłączyć *aptitude* przy pomocy ``[Ctrl]+[q]``

* **Wykonaj** aktualizację i **instalację** dodatkowych pakietów:

.. code-block:: sh

    aptitude update
    touch /boot/initrd.img-3.2.0-1455-omap4
    aptitude full-upgrade
    aptitude install -y
    aptitude install -y wireless-crda wireless-regdb # dodatkowe pakiety do obsługi sieci bezprzewodowej
    aptitude install -y htop psmisc mc unzip bash-completion cpufrequtils ntp # dodatkowe narzędzia
    aptitude install -y byobu tmux

.. warning::

    Instalacja jądra systemu wymaga obecności plików w katalogu ``/boot/``. W razie ich braku, wystarczy stworzyć brakujący plik przy pomocy polecenia ``touch``.

* **Dodaj** do pliku ``/etc/rc.local`` linijkę ``iw reg set PL``.
* **Wyłącz** system przy pomocy polecenia ``sudo poweroff``.

Aktualizacja bootloadera
~~~~~~~~~~~~~~~~~~~~~~~~

Aby karta uruchamiała się na płytkach w wersji **B3**, należy pobrać ostatnią wersję bootloadera *u-boot* i manualnie go skompilować:

.. code-block: sh

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
    $ cat > boot.script
    fatload mmc 0:1 0x80000000 uImage
    setenv bootargs rw vram=32M fixrtc mem=1G@0x80000000 root=/dev/mmcblk0p2 console=ttyO2,115200n8 rootwait
    bootm 0x80000000
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

Wynikiem wykonania tych operacji będą pliki, które należy umieścić na pierwszej partycji zamontowanej karty:

* boot.scr
* boot.script
* MLO
* u-boot.bin
* u-boot.img
