Przygotowanie do uruchomienia
=============================

Wgranie obrazu systemu na kartę
-------------------------------

* **Pobierz** obraz `Ubuntu Server 12.04 amrhf+omap4`_ dla PandaBoard ze strony `Ubuntu`_.

.. seealso::

    Więcej informacji na temat wsparcia Ubuntu dla płyt opartych o OMAP dostępne jest na stronie `ARM/OMAP`_.

* **Sprawdź** sumy kontrolne *md5* z dostępnymi na `serwerze`_ obrazów.
* **Sprawdź** czy karta SD jest w trybie *do zapisu*.

.. note::

    Przełącznik zapisu powinien być przesunięty do góry, gdzie u góry karty znajdują są styki.

* **Umieść** kartę w czytniku kart komputera.
* **Wywołaj** jedno z poniższych zestawów poleceń:

.. code-block:: sh

    gunzip -c ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz | sudo dd bs=1M of=/dev/<device name>
    sync

lub:

.. code-block:: sh

    sudo sh -c 'zcat ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz > /dev/<device name>'
    sync

``<device name`` powinno być zastąpione nazwą urządzenia blokowego.

* **Wyciągnij** kartę z czytnika kart komputera.
* **Umieść** kartę w czytniku kart *PandaBoard*.

.. _Ubuntu Server 12.04 amrhf+omap4: http://cdimage.ubuntu.com/releases/12.04/release/ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz
.. _Ubuntu: http://cdimage.ubuntu.com/releases/12.04/release/
.. _serwerze: http://cdimage.ubuntu.com/releases/12.04/release/MD5SUMS
.. _ARM/OMAP: https://wiki.ubuntu.com/ARM/OMAP
