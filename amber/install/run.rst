Uruchomienie
~~~~~~~~~~~~

* **Skopiować** przykładowy plik konfiguracyjny:

.. code-block:: sh

    cp ${HOME}/amber/amber-erlang-mediator/apps/amber/priv/settings.config.example ${HOME}/amber/amber-erlang-mediator/apps/amber/priv/settings.config

* **Uruchomić** ``${HOME}/amber/amber-erlang-mediator/start_amber.sh``

Aby zakończyć pracę mediatora, należy wywołać polecenie ``killall heart``. Logi aplikacji znajdują się w ``${HOME}/amber/amber-main/log*``.

.. note::

    Możliwe jest uruchomienie w trybie deweloperskim. Jest to standardowe uruchomienie mediatora, z włączonymi przeglądaniem logów oraz zamknięciem mediatora, po przerwaniu przeglądania logów ``[Ctrl]+[c]``. Wywoływane jest przez polecenie ``${HOME}/amber/amber-main/start_devel_amber.sh``.
