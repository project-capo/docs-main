Dokumentacja mgr-docs!
======================

Jest to dokumentacja opisująca korzystanie z projektów:

* `amber-main`_ jest to projekt mediatora, który to dostarcza mechanizmu komunikacji pomiędzy poszczególnymi sterownikami oraz klientami
* `amber-cpp-drivers`_ jest to projekt sterowników, napisanych w C/C++, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:
 * Roboclaw - sterowanie silnikami robota
 * Ninedof - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji z przyspieszeniomierza, żyroskopu oraz magnetometru
* `amber-python-drivers`_ jest to projekt sterowników, napisanych w python, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:
 * Roboclaw - sterowanie silnikami robota
 * Hokuyo - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji o odległościach innych przeszkód od robota
* `amber-java-clients`_ - jest to projekt dostarczają klientów, napisanych w Java, używanych przez korzystających z robota, w ich własnych aplikacjach, obsługiwane są:
 * Roboclaw
 * Hokuyo
 * Ninedof
* `amber-python-clients`_ jest to projekt dostarczają klientów, napisanych w python, używanych przez korzystających z robota, w ich własnych aplikacjach, obsługiwane są:
 * Roboclaw
 * Hokuyo
 * Ninedof
* `amber-common`_ jest to projekt zawierający część wspólną wyżej wymienionych projektów, którymi są:
 * pliki opisu ProtoBuf

.. _amber-main: https://github.com/dev-amber/amber-main
.. _amber-cpp-drivers: https://github.com/dev-amber/amber-cpp-drivers
.. _amber-python-drivers: https://github.com/dev-amber/amber-python-drivers
.. _amber-java-clients: https://github.com/dev-amber/amber-java-clients
.. _amber-python-clients: https://github.com/dev-amber/amber-python-clients
.. _amber-common: https://github.com/dev-amber/amber-common

Zawartość
---------

* :ref:`amber-docs`
* :ref:`navi-docs`

.. _amber-docs:

Amber
~~~~~

.. toctree::
    :maxdepth: 2

    amber/index
    amber/getting_started
    amber/installation
    amber/settings
    amber/mediator
    amber/drivers
    amber/clients
    amber/support

.. _navi-docs:

Navi
~~~~

.. toctree::
    :maxdepth: 2

    navi/index