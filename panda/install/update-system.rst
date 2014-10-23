Aktualizacja systemu
--------------------

* **Zainstalować** *screen* poprzez ``aptitude install screen``.
* **Uruchomić** *screen* poprzez ``screen``.
* **Zaktualizować** system poprzez ``do-release-upgrade``.

.. note::

    Proces aktualizacji może trwać długo. Z wykorzystaniem screen możliwe jest odłączenie się od konsoli poprzez kombinacje klawiszy ``[Ctrl]+[a]`` i ``[d]``. Ponownie podłączenie poprzez polecenie ``screen -r``.

.. warning::

    Proszę monitorować stan aktualizacji. W trakcie aktualizacji pojawiać się będą pytania do akceptacji lub nie. Po zakończeniu procesu aktualizacji system zostanie uruchomiony ponownie, co wymaga potwierdzenia.

Polecam **wyłączyć** opcję instalowania polecanych pakietów w *aptitude*:

* Uruchomić ``aptitude``.
* Skrót klawiszowy [Ctrl]+[t]
* Wybór menu ``Options`` → ``Preferences``
* Odznaczyć ``Install recommended packages automatically``

.. seealso::

    Interesującym miejscem, gdzie znajdują się pakiety używane na PandaBoard jest http://ports.ubuntu.com/ w `linux-ti-omap`_.


Po wykonaniu aktualizacji, system nie wspiera WiFi. Należy **dodać** do repozytorium *apt* repozytoriów *omap*. Następnie wykonać **aktualizację** listy pakietów i **instalację** następujących pakietów:

.. code-block:: sh

    aptitude install -y software-properties-common
    add-apt-repository ppa:tiomap-dev/release
    aptitude update
    touch /boot/initrd.img-3.13.0-37-generic
    aptitude install linux-headers-omap linux-image-omap linux-omap

**Wykonać** ``reboot``. Po ponownym uruchomieniu systemu, **wykonać** aktualizaję i **instalację** dodatkowych pakietów:

.. code-block:: sh

    aptitude update
    aptitude install -y
    aptitude install -y wpasupplicant wireless-tools # do obsługi sieci bezprzewodowej
    aptitude install -y htop psmisc mc unzip bash-completion cpufrequtils ntp # dodatkowe narzędzia

* **Zmienić** ustawienia sieci, w pliku ``/etc/network/interfaces`` - dodać ustawienia sieci bezprzewodowej:

.. code-block::

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

.. note::

    Powyższe ustawienia sieci bezprzewodowej dotyczą sieci bezprzewodowej *Robolab* w laboratorium. Aktualne hasło do sieci *Robolab* udostępnione jest w laboratorium, w ogłoszeniach znajdujących się w widocznym miejscu. Adresy przydzielane są w oparciu o adresy MAC urządzeń bezprzewodowych. W sieci laboratoryjnej prefiksem MAC jest ``de:ad:be:ef:00:**``. Ostatnie dwa znaki heksadecymalne określają przypisywany adres IP, według następującego schematu:

    ::
    
        de:ad:be:ef:00:00 - 192.168.2.200
        de:ad:be:ef:00:01 - 192.168.2.201
        ...
        de:ad:be:ef:00:09 - 192.168.2.209
        de:ad:be:ef:00:10 - 192.168.2.210

* **Zrestartować** system.
* **Połączyć** się podając przydzielony przez router adres IP. *Polecam* sprawdzić przypisany adres IP poprzez interfejs administratora routera.

.. _linux-ti-omap: http://ports.ubuntu.com/pool/main/l/linux-ti-omap4/
