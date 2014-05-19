Instalacja
==========

* Pobrać obraz `Ubuntu Server 12.04`_ dla PandaBoard z strony `Ubuntu`_.
* Sprawdzić sumy kontroler md5 z dostępnymi na `serwerze`_.
* Umieścić kartę w czytniki kart
* Wywołać jeden z poniższych poleceń
::

    gunzip -c ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz | sudo dd bs=1M of=/dev/<device name>
    sync

lub
::

    sudo sh -c 'zcat ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz > /dev/<device name>'
    sync

* Wyciągnąć kartę z czytnika i umieścić w PandaBoard, po czym uruchomić PandaBoard.

Pierwsze ładowanie systemu spowoduje, że partycja z systemem rozszerzy się do wielkości karty. Nie należy przerywać uruchomiania systemu. Należy odczekać, aż do momentu, gdy jedna z diod na płytce będzie mrugała cyklicznie. Po tym można wyłączyć płytkę i usunąć kartę z płytki, umieszczając ją z powrotem do czytnika w komputerze.

* Zmienić plik odpowiedzialny za sieć: ``/etc/network/interfaces``
::

    # interfaces(5) file used by ifup(8) and ifdown(8)
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
        address 192.168.2.50
        netmask 255.255.255.0
        gateway 192.168.2.1

* Zmienić plik odpowiedzialny za DNS: ``/etc/resolv.conf``
::

    nameserver 8.8.8.8

* Zmienić plik: ``/etc/rc.local``
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

* Zmienić plik odpowiedzialne za hasła, usuwając x lub * z pola na hasło: ``/etc/passwd`` i ``/etc/shadow``
::

    #!/etc/passwd
    root::0:0:root:/root:/bin/bash

    #!/etc/shadow
    root::15454:0:99999:7:::

* Umieścić swój klucz publiczny SSH w ``/root/.ssh/authorized_keys``
::

    ssh-rsa AAA... user@hostname

* Wyciągnąć z czytnika, po uprzednim odmontowaniu.
* Ponownie uruchamić płytkę z kartą.

Czekamy aż się załaduje i zainstaluje.

* Płytkę połączyć kablem sieciowym z siecią.
* Zalogować się do systemu poprzez ssh: ``ssh root@192.168.2.50``.
* Zaktualizować system poprzez **aptitude**.

Polecam wykonać tę operację przez ``aptitude``. Początkowo należy pobrać nowe informacje z repozytorium, poprzez ``aptitude update``. Następnie, korzystając z UI, zaktualizować istniejące pakiety z najmniej nowo instalowanym pakietami. Polecam wyłączyć opcję instalowania polecanych pakietów. Wymaga przeładowania aplikacji.

* Zainstalować sterowniki do WiFi, korzystając z dostępnych w repozytorium Ubuntu.
* Ustawić hasło dla użytkownika root przy pomocy ``passwd``.

.. _Ubuntu Server 12.04: http://cdimage.ubuntu.com/releases/12.04/release/ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz
.. _Ubuntu: http://cdimage.ubuntu.com/releases/12.04/release/
.. _serwerze: http://cdimage.ubuntu.com/releases/12.04/release/MD5SUMS

Dodatkowe informacje
--------------------

Więcej informacji na

* `Wiki/ARM/OMAP`_
* `Wiki/ARM/Server/Install`_

.. _Wiki/ARM/OMAP: https://wiki.ubuntu.com/ARM/OMAP
.. _Wiki/ARM/Server/Install: https://wiki.ubuntu.com/ARM/Server/Install