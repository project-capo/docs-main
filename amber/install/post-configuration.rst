Post-konfiguracja
-----------------

* **Odkomentować** ostatnią linijkę w ``/etc/rc.local``:

.. code-block:: sh

    ...

    su - panda -c "/home/panda/amber/amber-erlang-mediator/start_amber.sh"

    exit 0

* **Skopiować** przykładowy plik konfiguracyjny:

.. code-block:: sh

    cp ${HOME}/amber/amber-erlang-mediator/apps/amber/priv/settings.config.example ${HOME}/amber/amber-erlang-mediator/apps/amber/priv/settings.config
