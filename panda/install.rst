Instalacja
==========

Instrukcja
----------

* **Pobrać** obraz `Ubuntu Server 12.04 amrhf+omap4`_ dla PandaBoard z strony `Ubuntu`_.
* **Sprawdzić** sumy kontroler md5 z dostępnymi na `serwerze`_.
* *Umieścić* kartę w czytniku kart.
* *Wywołać* jeden z poniższych poleceń.
::

    gunzip -c ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz | sudo dd bs=1M of=/dev/<device name>
    sync

lub
::

    sudo sh -c 'zcat ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz > /dev/<device name>'
    sync

* *Wyciągnąć* kartę z czytnika.
* *Umieścić* w PandaBoard.
* *Uruchomić* PandaBoard.

Pierwsze ładowanie systemu spowoduje, że partycja z systemem rozszerzy się do wielkości karty. **Nie należy przerywać** uruchomiania systemu. **Należy czekać** do momentu, gdy jedna z diod na płytce będzie mrugała cyklicznie. Można *wyłączyć* płytkę, *wyciągnąć* kartę z płytki i *umieścić* ją w czytniku.

* **Zmienić** plik odpowiedzialny za sieć: ``/etc/network/interfaces``
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

* **Zmienić** plik: ``/etc/rc.local``
::

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

    yes | apt-get install openssh-server

    exit 0

* **Zmienić** plik odpowiedzialne za hasła, usuwając znaki ``x`` lub ``*`` z pól odpowiedzialnych za hasło ``/etc/passwd`` i ``/etc/shadow``
::

    #~/etc/passwd
    root::0:0:root:/root:/bin/bash

    #~/etc/shadow
    root::15454:0:99999:7:::

* **Dodać** swój klucz publiczny SSH w ``/root/.ssh/authorized_keys``
::

    ssh-rsa AAA... user@hostname

* **Odmontować** kartę pamięci.
* *Wyciągnąć* kartę z czytnika.
* *Umieścić* w PandaBoard.
* *Uruchomić* PandaBoard.

Powyższe operacje spowodują, że system umieszczony na płytce, połączy się z siecią lokalną (tutaj z siecią ``192.168.2.0/24`` i bramą domyślną ``192.168.2.1``) i wykona operację instalacji serwera SSH. Dzięki temu, można się zalogować do systemu przez sieć lokalną.

* **Połączyć** płytkę, kablem sieciowym, z siecią.
* *Zalogować* się do systemu poprzez ssh: ``ssh root@192.168.2.50``.

Następnie należy **przerwać** konfigurację płytki z wykorzystaniem kreatora.

* **Wywołać** polecenie ``fuser -k /var/cache/debconf/config.dat`` do oporu.
* **Usunąć** pakiet ``oem-config`` oraz katalog ``/var/lib/oem-config``.
* **Zrestartować** system.

* **Ustawić** hasło dla użytkownika root przy pomocy ``passwd``.
* **Ustawić** nazwę systemu w plikach ``/etc/hostname`` i ``/etc/hosts``.
::

    #~/etc/hostname
    panda.robonet

    #~/etc/hosts
    127.0.0.1 localhost
    127.0.1.1 panda panda.robonet

* **Zaktualizować** system poprzez **aptitude**.

Polecam wykonać tę operację przez ``aptitude``. Początkowo należy pobrać nowe informacje z repozytorium, poprzez ``aptitude update``. Następnie, korzystając z UI, zaktualizować istniejące pakiety, z najmniej nowo instalowanym pakietami. Polecam wyłączyć opcję instalowania polecanych pakietów. Wymaga zrestartowania aplikacji.

* *Zainstalować* dodatkowe oprogramowanie, jak na przykład: ``htop``, ``psmisc``, ``mc``, ``unzip``, ``screen``, ``bash-completion``.

* **Zainstalować** ``wpasupplicant``.
* **Zmienić** ustawienia sieci, w pliku ``/etc/network/interfaces``, ustawienia WiFi
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
        wpa-psk  "PASS"

* **Zrestartować** system.
* *Połączyć* się podając przydzielony przez router adres IP.

Powyższa instrukcja pozwala na utworzenie czystego i zaktualizowanego systemu Ubuntu 12.04.4 dla Panda Board. Do pracy z platformą Amber potrzebne są dodatkowe narzędzia, takie jak
::

    git, make
    erlang
    python, python-dev, python-setuptools, python-pip, python-virtualenv
    g++, libcxxtools-dev
    libboost-dev, liblog4cxx10-dev, libboost-program-options-dev, libboost-thread-dev
    protobuf-compiler, libprotoc-dev,


W celu instalacji erlanga, potrzeba dodać repozytoria ``backports`` i ``updates`` oraz zmienić wersję z ``precise`` na ``raring``, *tymczasowo*. Zainstalować i wrócić do poprzedniej wersji systemu.

* **Dodać** użytkownika ``panda``.
* **Zmienić** zawartość pliku ``/etc/rc.local``
::

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

    cpufreq-set -g performance

    # Enable GPIO_136 and use it as output
    echo 0x03 > /sys/kernel/debug/omap_mux/mcspi1_simo
    echo 0x03 > /sys/kernel/debug/omap_mux/mcspi1_cs0
    echo 0x03 > /sys/kernel/debug/omap_mux/mcspi1_cs2

    # Export GPIO_136 to userspace
    echo 136 > /sys/class/gpio/export
    echo 137 > /sys/class/gpio/export
    echo 139 > /sys/class/gpio/export

    # Change pin direction to out
    echo out > /sys/class/gpio/gpio136/direction
    echo out > /sys/class/gpio/gpio137/direction
    echo out > /sys/class/gpio/gpio139/direction

    # Put it high
    echo 1 > /sys/class/gpio/gpio136/value
    echo 1 > /sys/class/gpio/gpio137/value
    echo 1 > /sys/class/gpio/gpio139/value

    # Permissions
    chgrp dialout /sys/class/gpio/gpio136/*
    chmod g+w /sys/class/gpio/gpio136/*

    chgrp dialout /sys/class/gpio/gpio137/*
    chmod g+w /sys/class/gpio/gpio137/*

    chgrp dialout /sys/class/gpio/gpio139/*
    chmod g+w /sys/class/gpio/gpio139/*

    #su - panda -c "/home/panda/amber/amber-main/start_amber.sh"

    exit 0

* **Zalogować** się na użytkownika ``panda``: ``su - panda``.
* **Dodać** swój klucz publiczny SSH w ``/home/panda/.ssh/authorized_keys``
::

    ssh-rsa AAA... user@hostname

Następnie należy pobrać i zainstalować Amber wraz z dodatkami.
::

    mkdir -p ${HOME}/amber
    pushd ${HOME}/amber
        git clone https://github.com/dev-amber/amber-cpp-drivers.git
        pushd ${HOME}/amber/amber-cpp-drivers
            make clean
            make all
        popd
        git clone https://github.com/dev-amber/amber-python-drivers.git
        pushd ${HOME}/amber/amber-python-drivers
            ${HOME}/amber/amber-python-drivers/install.sh
        popd
        git clone https://github.com/dev-amber/amber-main.git
        pushd ${HOME}/amber/amber-main
            make all
        popd
    popd

* *Odkomentować* ostatnią linijkę w ``/etc/rc.local``.
* **Wyedtować** plik konfiguracyjny

    pushd ${HOME}/amber/amber-main/apps/amber/priv/
        cp settings.config.example settings.config
        nano settings.config
    popd

* **Uruchomić** ``/home/panda/amber/amber-main/start_amber.sh``

.. _Ubuntu Server 12.04 amrhf+omap4: http://cdimage.ubuntu.com/releases/12.04/release/ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz
.. _Ubuntu: http://cdimage.ubuntu.com/releases/12.04/release/
.. _serwerze: http://cdimage.ubuntu.com/releases/12.04/release/MD5SUMS

Dodatkowe informacje
--------------------

Więcej informacji na

* `Wiki/ARM/OMAP`_
* `Wiki/ARM/Server/Install`_

.. _Wiki/ARM/OMAP: https://wiki.ubuntu.com/ARM/OMAP
.. _Wiki/ARM/Server/Install: https://wiki.ubuntu.com/ARM/Server/Install