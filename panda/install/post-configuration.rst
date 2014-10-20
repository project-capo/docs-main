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
