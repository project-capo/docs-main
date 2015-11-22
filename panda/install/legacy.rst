Pierwsze uruchomienie instalacyjne
----------------------------------

Pierwsze ładowanie systemu spowoduje, że partycja z systemem rozszerzy się do wielkości karty. **Nie należy przerywać** uruchamiania systemu. **Należy czekać** do momentu, gdy jedna z diod na płytce będzie mrugała cyklicznie.

.. note::

    Jeśli posiadasz monitor z wejściem HDMI oraz klawiaturę lub port komunikacji szeregowej, dalszy proces instalacji możesz wykonać zgodnie z instrukacjami pojawiającymi się na ekranie. Jeśli nie posiadasz, możliwe jest dokończenie instalacji systemu według poniższej instrukcji.

* **Włącz** *PandaBoard*.
* **Czekaj** do momentu, gdy jedna z diod będzie mrugała cyklicznie.
* **Wyłącz** *PandaBoard*.
* **Wyciągnij** kartę z czytnika z *PandaBoard*.
* **Umieść** kartę w czytniku kart komputera.

Przygotowanie systemu do konfiguracji
-------------------------------------

* **Zamontuj** partycję systemową (drugą).
* **Zmień** plik odpowiedzialny za ustawienia sieci, znajdujący się na partycji systemowej, pod ścieżką ``/etc/network/interfaces``.

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

    Powyższa konfiguracja powoduje przypisanie adresu ``192.168.2.50`` w sieci ``192.168.2.0/24`` do interfejsu sieci przewodowej znajdującego się na płytce. Dodatkowo, ustawiona jest brama domyślna o adresie ``192.168.2.1`` oraz serwer nazw DNS ``8.8.8.8``.

.. warning::

    **Uwaga!** Powyższa adresacja IPv4 stosowana jest w sieci w laboratorium. W twoim przypadku może być ona inna. Proszę, zwróć uwagę na adresację Twojej sieci.

.. warning::

    Adresacja sieci ``192.168.2.0/24`` **docelowo** jest używana na interfejsie karty bezprzewodowej w laboratorium. Powyższa konfiguracja ulega zmianie w toku wykonywania tej instrukcji, w kroku `aktualizacji`_ ustawień sieciowych.

.. _aktualizacji: #updatenetwork

* **Zmień** plik znajdujący się na partycji systemowej, pod ścieżką ``/etc/rc.local``.

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

    Powyższa konfiguracja spowoduje zainstalowanie serwera zdalnego dostępu SSH w trakcie uruchomienia systemu. Należy pamiętać, aby po pierwszym zalogowaniu usunąć linijkę ``apt-get...`` z pliku ``/etc/rc.local``.

* **Zmień** plik odpowiedzialne za hasła, usuwając znaki ``x`` lub ``*`` z pól odpowiedzialnych za hasło, w plikach znajdujących się na partycji systemowej ``/etc/passwd`` i ``/etc/shadow``

.. code-block:: sh

    #-/etc/passwd
    root::0:0:root:/root:/bin/bash

    #-/etc/shadow
    root::15454:0:99999:7:::

.. note::

    Powyższe zmiany spowodują usunięcie hasła dla konta ``root``. Przy pierwszym logowaniu należy pamiętać o ustawieniu hasła dla administratora.

* **Dodaj** swój klucz publiczny SSH w ``/root/.ssh/authorized_keys``

.. code-block:: sh

    ssh-rsa AAA... user@hostname

.. note::

    Twój klucz publiczny SSH znajduje się w pliku ``~/.ssh/id_rsa.pub``. Jeśli pliku nie posiadasz, oznacza to, że nie posiadasz klucza SSH. W celu wygenerowania klucza prywatnego i publicznego SSH należy wywołać polecenie ``ssh-keygen``.

* **Odmontuj** kartę z czytnika kart komputera.
* **Wyciągnij** kartę z czytnika kart komputera.
* **Połącz** płytkę, kablem sieciowym, z urządzeniem sieciowym (np. przełącznikiem) znajdującym się w sieci, w której znajduje się Twój komputer.
* **Umieść** kartę w czytniku kart *PandaBoard*.
* **Uruchom** *PandaBoard*.

Drugie uruchomienie konfiguracyjne
----------------------------------

* **Zaloguj** się do systemu poprzez SSH: ``ssh root@192.168.2.50``.
* **Ustaw** hasło dla użytkownika ``root`` przy pomocy ``passwd root``.
* **Usuń** linię ``apt-get install -y openssh-server`` z pliku ``/etc/rc.local``.
* **Ustaw** nazwę systemu w plikach:

``/etc/hostname``

.. code-block:: sh

    panda.robonet

``/etc/hosts``

.. code-block:: sh

    127.0.0.1 localhost
    127.0.1.1 panda panda.robonet

.. warning::

    Należy **przerwać** konfigurację płytki z wykorzystaniem kreatora, który działa na konsoli (dostępnej przy instalacji z wykorzystaniem monitora i klawiatury lub portu komunikacji szeregowej).

* **Wywołaj** polecenie ``fuser -k /var/cache/debconf/config.dat`` do oporu.
* **Usuń** pakiet ``oem-config`` (z wykorzystaniem ``aptitude`` - ``aptitude purge oem-config``) oraz katalog ``/var/lib/oem-config``.
* **Zrestartuj** system przy pomocy polecenia ``reboot``.

Aktualizacja oprogramowania
---------------------------

Aktualizacja systemu
~~~~~~~~~~~~~~~~~~~~

* **Zainstaluj** *screen* poprzez ``aptitude install screen``.
* **Uruchom** *screen* poprzez ``screen``.

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
    aptitude install -y wpasupplicant wireless-crda wireless-regdb # do obsługi sieci bezprzewodowej
    aptitude install -y htop psmisc mc unzip bash-completion cpufrequtils ntp # dodatkowe narzędzia
    aptitude install -y byobu tmux

.. warning::

    Instalacja jądra systemu wymaga obecności plików w katalogu ``/boot/``. W razie ich braku, wystarczy stworzyć brakujący plik przy pomocy polecenia ``touch``.

* **Dodaj** do pliku ``/etc/rc.local`` linijkę ``iw reg set PL``.

.. _updatenetwork:

* **Zmień** ustawienia sieci: do pliku ``/etc/network/interfaces`` dodaj ustawienia sieci bezprzewodowej:

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

    W celu poprawnego działania sieci bezprzewodowej wymagane jest ustawienie adresu MAC kart bezprzewodowej.

.. warning::

    Zwróć uwagę na fakt, że adresacja interfejsu sieci przewodowej została zmieniona, tak aby na dwóch interfejsach karty przewodowej i bezprzewodowej nie było takiej samej adresacji sieci.

.. note::

    Powyższe ustawienia sieci bezprzewodowej dotyczą sieci bezprzewodowej *robolab* w laboratorium. Aktualne hasło do sieci *robolab* udostępnione jest w laboratorium, w ogłoszeniach znajdujących się w widocznym miejscu. Adresy przydzielane są w oparciu o adresy MAC urządzeń bezprzewodowych. W sieci laboratoryjnej prefiksem MAC jest ``de:ad:be:ef:00:**``. Ostatnie dwa znaki heksadecymalne określają przypisywany adres IP, według następującego schematu:

    ::

        de:ad:be:ef:00:00 - 192.168.2.200
        de:ad:be:ef:00:01 - 192.168.2.201
        ...
        de:ad:be:ef:00:09 - 192.168.2.209
        de:ad:be:ef:00:10 - 192.168.2.210

* **Zrestartuj** system.
* **Połącz** się podając przydzielony przez router adres IP. *Polecam* sprawdzić przypisany adres IP poprzez interfejs administratora routera.

.. _linux-ti-omap: http://ports.ubuntu.com/pool/main/l/linux-ti-omap4/

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

* **Zwróć** uwagę na obecność skryptu ``/etc/init.d/ondemand``. Należy go wyłączyć poprzez ``update-rc.d -f ondemand remove``.
