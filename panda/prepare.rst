Prepare to run
==============

Write OS image to SD card
-------------------------

* **Download** `Ubuntu Server 12.04 amrhf+omap4`_ image for PandaBoard from website `Ubuntu`_.

.. seealso::

    More information about Ubuntu support for board based on OMAP are available on website `ARM/OMAP`_.

* **Check** *md5* sums with sums which are available on `server`_.
* **Check** if SD card is in *write mode*.

.. note::

    Write switch on card should be in **up** position, closed to contacts.

* **Insert** card in computer card reader.
* **Execute** one of following commands sets:

.. code-block:: sh

    gunzip -c ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz | sudo dd bs=1M of=/dev/<device name>
    sync

or:

.. code-block:: sh

    sudo sh -c 'zcat ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz > /dev/<device name>'
    sync

``<device name>`` should be replaced with the block device name.

* **Pull** card from card reader.
* **Insert** card *PandaBoard* card reader.

.. _Ubuntu Server 12.04 amrhf+omap4: http://cdimage.ubuntu.com/releases/12.04/release/ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz
.. _Ubuntu: http://cdimage.ubuntu.com/releases/12.04/release/
.. _server: http://cdimage.ubuntu.com/releases/12.04/release/MD5SUMS
.. _ARM/OMAP: https://wiki.ubuntu.com/ARM/OMAP
