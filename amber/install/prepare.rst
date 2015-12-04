Przygotowanie środowiska
------------------------

Instalacja dodatkowego oprogramowania
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    W *Ubuntu 12.04.5 LTS* należy dodać dodatkowe repozytoria pozwalające na zainstalowanie wspieranej przez Amber wersji Erlang. Należy dodać do pliku ``/etc/apt/sources.list``:

    .. code-block:: sh

        deb http://packages.erlang-solutions.com/debian wheezy contrib

    Po dodaniu wpisu należy wykonać ``aptitude update``. Jeśli wystąpią problemy z pobieraniem listy pakietów z powodu braku klucza, należy dodać klucz przy pomocy polecenia:

    .. code-block:: sh

        apt-key adv --recv-keys --keyserver keyserver.ubuntu.com D208507CA14F4FCA


Do pracy z platformą *Amber* potrzebne są dodatkowe narzędzia. Należy zainstalować powyższe narzędzia z wykorzystaniem polecenia ``aptitude install``:

.. code-block:: sh

    aptitude install -y git make
    aptitude install -y esl-erlang
    aptitude install -y g++ libcxxtools-dev liblog4cxx10-dev libboost-dev libboost-program-options-dev libboost-thread-dev libboost-system-dev
    aptitude install -y protobuf-compiler libprotoc-dev
    aptitude install -y python python-dev python-setuptools python-pip python-virtualenv

Modyfikacja plików konfiguracyjnych
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Dodać** wpis do pliku ``/etc/modules`` (jeśli nie zostało wykonane):

::

    ...
    i2c-dev

* **Zmienić** zawartość pliku ``/etc/rc.local``:

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
* **Dodać** użytkownika ``panda`` do grup ``dialout`` i ``sudo`` przy pomocy polecenia ``adduser panda dialout; adduser panda sudo``.

.. note::

    Plik odpowiedzialny za grupy użytkowników ``/etc/group``:

    .. code-block::

        ...
        dialout:x:20:panda
        ...
        sudo:x:27:panda
        ...

* **Zalogować** się na użytkownika ``panda``: ``su - panda``.
* **Dodać** swój klucz publiczny SSH do pliku ``/home/panda/.ssh/authorized_keys``

::

    ssh-rsa AAA... user@hostname
