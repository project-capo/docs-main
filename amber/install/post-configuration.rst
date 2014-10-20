* **Odkomentować** ostatnią linijkę w ``/etc/rc.local``:
::

    ...

    su - panda -c "/home/panda/amber/amber-erlang-mediator/start_amber.sh"

    exit 0

* **Zmienić** plik konfiguracyjny mediatora. Ustawienie sterowników obsługiwanych przez mediator:
::

    pushd ${HOME}/amber/amber-erlang-mediator/apps/amber/priv/
        cp settings.config.example settings.config
        nano settings.config
    popd
