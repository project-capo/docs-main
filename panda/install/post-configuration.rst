Post-konfiguracja
-----------------

* **Dodać** do ``/etc/modules`` wpis:

.. code-block::

    ...
    i2c-dev

* **Zmienić** ``/etc/init.d/cpufrequtils``:

.. code-block::

    ...
    GOVERNOR="performance"
    ...

* **Zwrócić** uwagę na obecność skryptu ``/etc/init.d/ondemand``. Należy go wyłączyć poprzez ``update-rc.d -f ondemand remove``.
