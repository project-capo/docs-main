Prepare environment
-------------------

Additional software installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    For *Ubuntu 12.04.5 LTS* need to add additional repository used to install supported by *Amber* Erlang verion. Following line need to be added to ``/etc/apt/sources.list``:

    .. code-block:: sh

        deb http://packages.erlang-solutions.com/debian wheezy contrib

    After adding this entry ``aptitude update`` need to be executed. If there will be some issues with downloading packages list key need to be added with following command:

    .. code-block:: sh

        apt-key adv --recv-keys --keyserver keyserver.ubuntu.com D208507CA14F4FCA

To work with *Amber* platform additional software need to be installed. Additional software can be installed with following commands:

.. code-block:: sh

    aptitude install -y git make
    aptitude install -y esl-erlang
    aptitude install -y g++ libcxxtools-dev liblog4cxx10-dev libboost-dev libboost-program-options-dev libboost-thread-dev libboost-system-dev
    aptitude install -y protobuf-compiler libprotoc-dev
    aptitude install -y python python-dev python-setuptools python-pip python-virtualenv

Configuration file modifications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Add** entry to file ``/etc/modules``:

::

    ...
    i2c-dev

* **Change** content of file ``/etc/rc.local``:

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

User creation
~~~~~~~~~~~~~

* **Create** user ``panda``.
* **Add** user ``panda`` to group ``dialout`` and ``sudo`` with commands ``adduser panda dialout; adduser panda sudo``.

.. note::

    File responsible for groups ``/etc/group``:

    .. code-block::

        ...
        dialout:x:20:panda
        ...
        sudo:x:27:panda
        ...

* **Login** with user ``panda``: ``su - panda``.
* **Add** your public SSH key to file ``/home/panda/.ssh/authorized_keys``

::

    ssh-rsa AAA... user@hostname
