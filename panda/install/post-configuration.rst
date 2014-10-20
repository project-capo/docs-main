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

* **Zwrócić** uwagę na obecność skryptu ``/etc/init.d/ondemand``. Należy go wyłączyć poprzez ``update-rc.d ondemand remove``.
