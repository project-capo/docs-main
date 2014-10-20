Przygotowanie środowiska
------------------------

Instalacja dodatkowego oprogramowania
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Do pracy z platformą *Amber* potrzebne są narzędzia:
::

    git make
    erlang
    g++ libcxxtools-dev liblog4cxx10-dev
    libboost-dev libboost-program-options-dev libboost-thread-dev libboost-system-dev
    protobuf-compiler libprotoc-dev
    python python-dev python-setuptools python-pip python-virtualenv

Należy zainstalować powyższe narzędzia z wykorzystaniem polecenia ``aptitude install``, np. ``aptitude install -y git make``.

Modyfikacja plików konfiguracyjnych
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Dodać** wpis do pliku ``/etc/modules`` (jeśli nie zostało wykonane):
::

    ...
    i2c-dev

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

    modprobe i2c-dev
    chown root:dialout /dev/i2c*
    chmod 660 /dev/i2c*

    #su - panda -c "/home/panda/amber/amber-erlang-mediator/start_amber.sh"

    exit 0

Utworzenie użytkownika
~~~~~~~~~~~~~~~~~~~~~~

* **Dodać** użytkownika ``panda``.
* **Dodać** użytkownika ``panda`` do grup ``dialout`` i ``sudo`` przy pomocy polecenia ``adduser panda dialout; adduser panda sudo``. Plik odpowiedzialny za grupy użytkowników ``/etc/group``:
::

    ...
    dialout:x:20:panda
    ...
    sudo:x:27:panda
    ...

* **Utworzyć** hasło dla użytkownika ``panda``: ``passwd panda``. Domyślny hasłem dla ``panda`` w *Robolab* jest hasło ``panda2013``.
* **Zalogować** się na użytkownika ``panda``: ``su - panda``.
* **Dodać** swój klucz publiczny SSH do pliku ``/home/panda/.ssh/authorized_keys``
::

    ssh-rsa AAA... user@hostname
