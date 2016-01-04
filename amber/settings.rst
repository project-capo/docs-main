Settings
========

Mediator
--------

To run mediator you need to configure drivers which will be started together with mediator. `Example configuration`_ should be adapted to new conditions and should be saved as file with name ``apps/amber/priv/settings.config``.

.. note::

    Currently fully supported are drivers for devices *Roboclaw*, *Ninedof*, *Hokuyo* and *Location*. These drivers can be uncommented in configuration filer ``apps/amber/priv/settings.config``.

.. _Example configuration: https://github.com/project-capo/amber-erlang-mediator/blob/master/apps/amber/priv/settings.config.example

Drivers
-------

Drivers and their configuration are managed by developers. Configuration is provided with drivers.

Klienci
-------

Clients and their configuration are managed by developers. Configuration is provided with clients.
