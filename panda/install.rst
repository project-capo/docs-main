Instalacja
==========

Instalacja systemu na karcie
----------------------------

* **Pobrać** obraz `Ubuntu Server 12.04 amrhf+omap4`_ dla PandaBoard z strony `Ubuntu`_. Więcej informacji na temat wsparcia Ubuntu dla płyt opartych o OMAP dostępne jest na stronie `ARM/OMAP`_.
* **Sprawdzić** sumy kontroler md5 z dostępnymi na `serwerze`_.
* **Sprawdź** czy karta SD jest w trybie *do zapisu*. Przełącznik powinien być przesunięty do góry, gdzie u góry karty znajdują są styki.
* **Umieścić** kartę w czytniku kart komputera.
* **Wywołać** jedno z poniższych poleceń:
::

    gunzip -c ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz | sudo dd bs=1M of=/dev/<device name>
    sync

lub:
::

    sudo sh -c 'zcat ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz > /dev/<device name>'
    sync

* **Wyciągnąć** kartę z czytnika kart komputera.
* **Umieścić** kartę w czytniku kart *PandaBoard*.
* **Uruchomić** *PandaBoard* wykorzystując oryginalny zasilacz prądu stałego 5V i natężeniu ~ 2.5A.

Pierwsze uruchomienie instalacyjne
----------------------------------

Pierwsze ładowanie systemu spowoduje, że partycja z systemem rozszerzy się do wielkości karty. **Nie należy przerywać** uruchamiania systemu. **Należy czekać** do momentu, gdy jedna z diod na płytce będzie mrugała cyklicznie.

Jeśli posiadasz monitor z wejściem HDMI oraz klawiaturę, dalszy proces instalacji możesz wykonać zgodnie z instrukacjami pojawiającymi się na ekranie. Jeśli nie posiadasz, możliwe jest dokończenie instalacji systemu według poniższej instrukcji.

* **Wyłączyć** *PandaBoard*.
* **Wyciągnąć** kartę z czytnika z *PandaBoard*.
* **Umieścić** kartę w czytniku kart komputera.

Przygotowanie systemu do konfiguracji
-------------------------------------

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

Powyższa konfiguracja dotyczy przypisania adresu ``192.168.2.50`` w sieci ``192.168.2.0/24`` do portu Ethernet znajdującego się na płytce. Dodatkowo, wskazywana jest brama domyślna o adresie ``192.168.2.1`` oraz serwer nazw DNS ``8.8.8.8``.

Uwaga: powyższa adresacja IPv4 stosowana jest w sieci *Robolab*. W twoim przypadku może być ona inna. Proszę, zwróć uwagę na adresację portu Ethernet.

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

    apt-get install -y openssh-server

    exit 0

Powyższa konfiguracja spowoduje zainstalowanie serwera zdalnego dostępu SSH w trakcie uruchomienia systemu. Należy pamiętać, by po pierwszym zalogowaniu usunąć linijkę ``apt-get...`` z pliku ``/etc/rc.local``.

* **Zmienić** plik odpowiedzialne za hasła, usuwając znaki ``x`` lub ``*`` z pól odpowiedzialnych za hasło ``/etc/passwd`` i ``/etc/shadow``
::

    #-/etc/passwd
    root::0:0:root:/root:/bin/bash

    #-/etc/shadow
    root::15454:0:99999:7:::

Powyższe zmiany powodują usunięcie hasła dla konta ``root``. Przy pierwszym logowaniu należy pamiętać o ustawieniu hasła dla administratora. Domyślny hasłem dla roota w *Robolab* jest ``panda2013``.

* **Dodać** swój klucz publiczny SSH w ``/root/.ssh/authorized_keys``
::

    ssh-rsa AAA... user@hostname

Twój klucz publiczny SSH znajduje się w pliku ``~/.ssh/id_rsa.pub``. Jeśli pliku nie posiadasz, oznacza to, że nie posiadasz klucza SSH. W celu wygenerowania klucza prywatnego i publicznego SSH należy wywołać polecenie ``ssh-keygen``.

* **Odmontować** kartę z czytnika kart komputera.
* **Wyciągnąć** kartę z czytnika kart komputera.
* **Połączyć** płytkę, kablem sieciowym, z siecią, w której znajduje się Twój komputer.
* **Umieścić** kartę w czytniku kart *PandaBoard*.
* **Uruchomić** *PandaBoard*.

Drugie uruchomienie konfiguracyjne
----------------------------------

* **Zalogować** się do systemu poprzez SSH: ``ssh root@192.168.2.50``.
* **Ustawić** hasło dla użytkownika ``root`` przy pomocy ``passwd``.
* **Usunąć** linię ``apt-get install -y openssh-server`` z pliku ``/etc/rc.local``.
* **Ustawić** nazwę systemu w plikach:

``/etc/hostname``
::

    panda.robonet

``/etc/hosts``
::

    127.0.0.1 localhost
    127.0.1.1 panda panda.robonet

Następnie należy **przerwać** konfigurację płytki z wykorzystaniem kreatora, który działa na konsoli (dostępnej przy instalacji z wykorzystaniem monitora i klawiatury).

* **Wywołać** polecenie ``fuser -k /var/cache/debconf/config.dat`` do oporu.
* **Usunąć** pakiet ``oem-config`` (z wykorzystaniem ``aptitude``) oraz katalog ``/var/lib/oem-config``.
* **Zrestartować** system poprzez ``reboot``.

Aktualizacja systemu
--------------------

* **Zainstalować** screen poprzez ``aptitude install screen``.
* **Uruchomić** screen.
* **Zaktualizować** system poprzez ``do-release-upgrade``.

Proces aktualizacji może trwać długo. Z wykorzystaniem screen możliwe jest odłączenie się od konsoli poprzez kombinacje klawiszy ``[Ctrl]+[a]`` i ``[d]``.

* **Zaktualizować** system poprzez **aptitude**.

**Polecam** wykonać tę operację przez ``aptitude``. **Polecam** wyłączyć opcję instalowania polecanych pakietów ([Ctrl]+[t] i wybór menu ``Options`` → ``Preferences`` i odznaczyć ``Install recommended packages automatically``). **Wymaga** zrestartowania aplikacji. Początkowo należy pobrać nowe informacje z repozytorium, poprzez ``aptitude update`` lub ``[u]``. Następnie, korzystając z UI, zaktualizować istniejące pakiety, z *najmniej* nowo instalowanym pakietami.

* **Zainstalować** ``wpasupplicant`` do obsługi sieci bezprzewodowej.
* **Zainstalować** dodatkowe oprogramowanie: ``htop``, ``psmisc``, ``mc``, ``unzip``, ``bash-completion``, ``cpufrequtils``.

* **Zmienić** ustawienia sieci, w pliku ``/etc/network/interfaces`` - dodać ustawienia sieci bezprzewodowej:
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
        wpa-ssid "Robolab"
        wpa-psk  "password"

W celu poprawnego działania sieci bezprzewodowej wymagane jest ustawienie adresu MAC kart bezprzewodowej.

Powyższe ustawienia sieci bezprzewodowej dotyczą sieci *Robolab*. Aktualne hasło do sieci *Robolab* udostępnione jest w laboratorium, w ogłoszeniach znajdujących się w widocznym miejscu. Adresy przydzielane są w oparciu o adresy MAC urządzeń bezprzewodowych. W sieci laboratoryjnej prefiksem MAC jest ``de:ad:be:ef:00:**``. Ostatnie dwa znaki heksadecymalne określają przypisywany adres IP, według następującego schematu:

    de:ad:be:ef:00:00 - 192.168.2.200
    de:ad:be:ef:00:01 - 192.168.2.201
    ...
    de:ad:be:ef:00:09 - 192.168.2.209
    de:ad:be:ef:00:10 - 192.168.2.210

* **Zrestartować** system.
* **Połączyć** się podając przydzielony przez router adres IP (*polecam* sprawdzić przypisany adres IP poprzez interfejs administratora routera).

Post-konfiguracja
-----------------

* **Dodać** do ``/etc/modules`` wpis:
::

    ...
    i2c-dev

* **Zmienić** ``/etc/init.d/cpufrequtils``:
::

    ...
    GOVERNOR="performance"
    ...

* **Zwrócić** uwagę na obecność skryptu ``/etc/init.d/ondemand``. Możliwe zmiany
 * Wywołać ``update-rc.d ondemand remove`` lub
 * W linii 27 pliku ``/etc/init.d/ondemand`` zmienić ``ondemand`` na ``performance``.

.. _Ubuntu Server 12.04 amrhf+omap4: http://cdimage.ubuntu.com/releases/12.04/release/ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz
.. _Ubuntu: http://cdimage.ubuntu.com/releases/12.04/release/
.. _serwerze: http://cdimage.ubuntu.com/releases/12.04/release/MD5SUMS
.. _ARM/OMAP: https://wiki.ubuntu.com/ARM/OMAP

Dodatkowe informacje
--------------------

Więcej informacji na stronach:

* `Wiki/ARM/OMAP`_
* `Wiki/ARM/Server/Install`_

.. _Wiki/ARM/OMAP: https://wiki.ubuntu.com/ARM/OMAP
.. _Wiki/ARM/Server/Install: https://wiki.ubuntu.com/ARM/Server/Install
