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
