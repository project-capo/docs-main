Amber
=====

Amber installation begins from `amber-erlang-mediator`_. It is a mediator, which is used in comunication between `drivers`_ and `clients`_.

In a normal scenario, there are following components:

* there is only one mediator
* there are different multiple drivers, which are communicating with different devices, there is no duplicated drivers
* there are multiple clients connected to mediator, which they use available devices

.. toctree::

    amber/install
    amber/settings
    amber/device_types
    amber/drivers
    amber/clients
    amber/communication

.. _drivers: ./amber/drivers.html
.. _clients: ./amber/clients.html
.. _amber-erlang-mediator: https://github.com/project-capo/amber-erlang-mediator
