Post-konfiguracja
-----------------

* **Dodać** do ``/etc/modules`` wpis:
::

    ...
    i2c-dev

* **Zmienić** ``/etc/init.d/cpufrequtils``:
::

    ...
    GOVERNOR="performance"
    ...

* **Zwrócić** uwagę na obecność skryptu ``/etc/init.d/ondemand``. Możliwe zmiany
 * Wywołać ``update-rc.d ondemand remove`` lub
 * W linii 27 pliku ``/etc/init.d/ondemand`` zmienić ``ondemand`` na ``performance``.

.. _Ubuntu Server 12.04 amrhf+omap4: http://cdimage.ubuntu.com/releases/12.04/release/ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz
.. _Ubuntu: http://cdimage.ubuntu.com/releases/12.04/release/
.. _serwerze: http://cdimage.ubuntu.com/releases/12.04/release/MD5SUMS
.. _ARM/OMAP: https://wiki.ubuntu.com/ARM/OMAP
