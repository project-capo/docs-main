Aktualizacja oprogramowania
---------------------------

Aktualizacja systemu
~~~~~~~~~~~~~~~~~~~~

* **Zainstalować** *screen* poprzez ``aptitude install screen``.
* **Uruchomić** *screen* poprzez ``screen``.

.. warning::

    Możliwe jest wykonanie aktualizacji do *Ubuntu 14.04.1* LTS przy pomocy polecenia ``do-release-upgrade``. Ze względu na problemy w obsłudze sterowników do *Ninedof* oraz *Roboclaw* jest to **niezalecane**. Można pominąć poniższe kroki do kroku aktualizacji_ pakietów.

.. note::

    Proces aktualizacji przy pomocy ``do-release-upgrade`` może trwać kilka minut. Z wykorzystaniem screen możliwe jest odłączenie się od konsoli poprzez kombinacje klawiszy ``[Ctrl]+[a]`` i ``[d]``. Ponownie podłączenie poprzez polecenie ``screen -r``.

.. warning::

    Proszę monitorować stan aktualizacji. W trakcie aktualizacji pojawiać się będą pytania do akceptacji lub nie. Po zakończeniu procesu aktualizacji system zostanie uruchomiony ponownie, co wymaga potwierdzenia.

.. seealso::

    Interesującym miejscem, gdzie znajdują się pakiety używane na PandaBoard jest http://ports.ubuntu.com/ w `linux-ti-omap`_.


Po wykonaniu aktualizacji przy pomocy ``do-release-upgrade``, system nie wspiera WiFi. Należy **dodać** do repozytorium *apt* repozytoriów *omap*. Następnie wykonać **aktualizację** listy pakietów i **instalację** następujących pakietów:

.. code-block:: sh

    aptitude install -y software-properties-common
    add-apt-repository ppa:tiomap-dev/release
    aptitude update
    touch /boot/initrd.img-3.13.0-37-generic
    aptitude install linux-headers-omap linux-image-omap linux-omap

.. warning::

    Instalacja jądra systemu wymaga obecności plików w katalogu `/boot/`. W razie ich braku, wystarczy stworzyć brakujący plik przy pomocy polecenia `touch`.

* **Wykonać** ``reboot``.

.. _aktualizacji:

Aktualizacja pakietów
~~~~~~~~~~~~~~~~~~~~~

Polecam **wyłączyć** opcję instalowania polecanych pakietów w *aptitude*:

* Uruchomić ``aptitude``.
* Skrót klawiszowy ``[Ctrl]+[t]``
* Wybór menu ``Options`` → ``Preferences``
* Odznaczyć ``Install recommended packages automatically``

* **Wykonać** aktualizację i **instalację** dodatkowych pakietów:

.. code-block:: sh

    aptitude update
    touch /boot/initrd.img-3.2.0-1455-omap4
    aptitude full-upgrade
    aptitude install -y
    aptitude install -y wpasupplicant wireless-tools wireless-crda wireless-regdb # do obsługi sieci bezprzewodowej
    aptitude install -y htop psmisc mc unzip bash-completion cpufrequtils ntp # dodatkowe narzędzia
    aptitude install -y byobu tmux

.. warning::

    Instalacja jądra systemu wymaga obecności plików w katalogu `/boot/`. W razie ich braku, wystarczy stworzyć brakujący plik przy pomocy polecenia `touch`.

* **Dodać** do pliku ``/etc/rc.local`` linijkę ``iw reg set PL``. 

.. _updatenetwork:

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
        wpa-ssid "robolab"
        wpa-psk  "password"

W celu poprawnego działania sieci bezprzewodowej wymagane jest ustawienie adresu MAC kart bezprzewodowej.

.. note::

    Powyższe ustawienia sieci bezprzewodowej dotyczą sieci bezprzewodowej *robolab* w laboratorium. Aktualne hasło do sieci *robolab* udostępnione jest w laboratorium, w ogłoszeniach znajdujących się w widocznym miejscu. Adresy przydzielane są w oparciu o adresy MAC urządzeń bezprzewodowych. W sieci laboratoryjnej prefiksem MAC jest ``de:ad:be:ef:00:**``. Ostatnie dwa znaki heksadecymalne określają przypisywany adres IP, według następującego schematu:

    ::
    
        de:ad:be:ef:00:00 - 192.168.2.200
        de:ad:be:ef:00:01 - 192.168.2.201
        ...
        de:ad:be:ef:00:09 - 192.168.2.209
        de:ad:be:ef:00:10 - 192.168.2.210

* **Zrestartować** system.
* **Połączyć** się podając przydzielony przez router adres IP. *Polecam* sprawdzić przypisany adres IP poprzez interfejs administratora routera.

.. _linux-ti-omap: http://ports.ubuntu.com/pool/main/l/linux-ti-omap4/
