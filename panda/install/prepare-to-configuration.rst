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

.. note::

    Powyższa konfiguracja dotyczy przypisania adresu ``192.168.2.50`` w sieci ``192.168.2.0/24`` do portu Ethernet znajdującego się na płytce. Dodatkowo, wskazywana jest brama domyślna o adresie ``192.168.2.1`` oraz serwer nazw DNS ``8.8.8.8``.

.. warning::

    Adresacja sieci ``192.168.2.0/24`` **docelowo** jest używana na interfejsie karty bezprzewodowej. Powyższa konfiguracja ulega zmianie w toku wykonywania tej instrukcji, w kroku `aktualizacji` ustawień sieciowych.

.. _aktualizacji: update-system.html#updatenetwork

.. warning::

    **Uwaga!** Powyższa adresacja IPv4 stosowana jest w sieci w laboratorium. W twoim przypadku może być ona inna. Proszę, zwróć uwagę na adresację portu Ethernet.

* **Zmienić** plik: ``/etc/rc.local``

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

    Powyższa konfiguracja spowoduje zainstalowanie serwera zdalnego dostępu SSH w trakcie uruchomienia systemu. Należy pamiętać, by po pierwszym zalogowaniu usunąć linijkę ``apt-get...`` z pliku ``/etc/rc.local``.

* **Zmienić** plik odpowiedzialne za hasła, usuwając znaki ``x`` lub ``*`` z pól odpowiedzialnych za hasło ``/etc/passwd`` i ``/etc/shadow``

.. code-block:: sh

    #-/etc/passwd
    root::0:0:root:/root:/bin/bash

    #-/etc/shadow
    root::15454:0:99999:7:::

.. note::

    Powyższe zmiany powodują usunięcie hasła dla konta ``root``. Przy pierwszym logowaniu należy pamiętać o ustawieniu hasła dla administratora. Domyślny hasłem dla roota w laboratorium jest ``panda2013``.

* **Dodać** swój klucz publiczny SSH w ``/root/.ssh/authorized_keys``

.. code-block:: sh

    ssh-rsa AAA... user@hostname

.. note::

    Twój klucz publiczny SSH znajduje się w pliku ``~/.ssh/id_rsa.pub``. Jeśli pliku nie posiadasz, oznacza to, że nie posiadasz klucza SSH. W celu wygenerowania klucza prywatnego i publicznego SSH należy wywołać polecenie ``ssh-keygen``.

* **Odmontować** kartę z czytnika kart komputera.
* **Wyciągnąć** kartę z czytnika kart komputera.
* **Połączyć** płytkę, kablem sieciowym, z urządzeniem sieciowym (np. przełącznikiem) znajdującym się w sieci, w której znajduje się Twój komputer.
* **Umieścić** kartę w czytniku kart *PandaBoard*.
* **Uruchomić** *PandaBoard*.
