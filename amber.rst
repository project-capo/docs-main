Amber
=====

Komponenty Amber zaczynają się od `amber-erlang-mediator`_. Jest to projekt mediatora, który to dostarcza mechanizmu komunikacji pomiędzy poszczególnymi `sterownikami`_ oraz `klientami`_.

W standardowym modelu zakłada się, że:

* istnieje jeden mediator
* używanych jest kilka sterowników, z których każdy komunikuje się z innym urządzeniem, nie ma sterowników duplikujących działanie
* podłączonych jest jeden lub wielu klientów, którzy korzystają jednocześnie z dostępnych urządzeń

.. toctree::

    amber/install
    amber/settings
    amber/device_types
    amber/drivers
    amber/clients
    amber/communication

.. _sterownikami: ./amber/drivers.html
.. _klientami: ./amber/clients.html
.. _amber-erlang-mediator: https://github.com/project-capo/amber-erlang-mediator
