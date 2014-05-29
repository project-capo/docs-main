Uruchomienie
============

Instalacja platformy Amber
~~~~~~~~~~~~~~~~~~~~~~~~~~

Powyższa instrukcja pozwala na utworzenie czystego i zaktualizowanego systemu *Ubuntu 12.04.4* dla Panda Board. Do pracy z platformą *Amber* potrzebne są dodatkowe narzędzia:
::

    git, make
    erlang
    python, python-dev, python-setuptools, python-pip, python-virtualenv
    g++, libcxxtools-dev
    libboost-dev, liblog4cxx10-dev, libboost-program-options-dev, libboost-thread-dev
    protobuf-compiler, libprotoc-dev


W celu instalacji erlanga, potrzeba dodać repozytoria ``backports`` i ``updates`` oraz zmienić wersję z ``precise`` na ``raring``, *tymczasowo*. Zainstalować i wrócić do poprzedniej wersji systemu.

* **Zmienić** ``/etc/modules`` (jeśli nie zostało wykonane):
::

    ...
    i2c-dev

* **Zmienić** ``/etc/init.d/cpufrequtils`` (jeśli nie zostało wykonane):
::

    ...
    GOVERNOR="performance"
    ...

* **Dodać** użytkownika ``panda``.
* **Zmienić** plik odpowiedzialny za grupy użytkowników ``/etc/groups``:
::

    ...
    dialout:x:20:panda
    ...

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

    #su - panda -c "/home/panda/amber/amber-main/start_amber.sh"

    exit 0

* **Zalogować** się na użytkownika ``panda``: ``su - panda``.
* **Dodać** swój klucz publiczny SSH w ``/home/panda/.ssh/authorized_keys``
::

    ssh-rsa AAA... user@hostname

Następnie należy pobrać i zainstalować *Amber* wraz z dodatkami.
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

* **Odkomentować** ostatnią linijkę w ``/etc/rc.local``:
::

    ...

    su - panda -c "/home/panda/amber/amber-main/start_amber.sh"

    exit 0

* **Zmienić** plik konfiguracyjny mediatora. Ustawienie sterowników obsługiwanych przez mediator:
::

    pushd ${HOME}/amber/amber-main/apps/amber/priv/
        cp settings.config.example settings.config
        nano settings.config
    popd

* **Uruchomić** ``${HOME}/amber/amber-main/start_amber.sh``

Aby zakończyć pracę mediatora, należy wywołać polecenie ``killall heart``. Logi aplikacji znajdują się w ``${HOME}/amber/amber-main/log``.

Możliwe jest uruchomienie w trybie deweloperskim. Jest to standardowe uruchomienie mediatora, z włączonymi przeglądaniem logów oraz zamknięciem mediatora, po przerwaniu przeglądania logów ``[Ctrl]+[c]``. Wywoływane jest przez polecenie ``${HOME}/amber/amber-main/start_devel_amber.sh``.