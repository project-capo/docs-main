Post-configuration
------------------

* **Uncomment** following line in file ``/etc/rc.local``:

.. code-block:: sh

    ...

    su - panda -c "/home/panda/amber/amber-erlang-mediator/start_amber.sh"

    exit 0

* **Copy** example configuration file:

.. code-block:: sh

    cp ${HOME}/amber/amber-erlang-mediator/apps/amber/priv/settings.config.example ${HOME}/amber/amber-erlang-mediator/apps/amber/priv/settings.config
