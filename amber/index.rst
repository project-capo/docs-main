Amber
=====

Repozytoria `Amber`_ zaczynamy od `amber-main`_: jest to projekt mediatora, który to dostarcza mechanizmu komunikacji pomiędzy poszczególnymi `sterownikami`_ oraz `klientami`_.

W standardowym modelu zakłada się, że:

* istnieje jeden mediator
* używanych jest kilka sterowników, z których każdy komunikuje się z innym urządzeniem (nie ma sterowników duplikujących działanie)
* podłączonych jest jeden lub wielu klientów, którzy korzystają z dostępnych urządzeń, jednocześnie

Sterowniki
----------

* `amber-cpp-drivers`_ jest to projekt sterowników, napisanych w *C/C++*, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:
 * **Roboclaw** - sterowanie silnikami robota
 * **Ninedof** - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji z przyspieszeniomierza, żyroskopu oraz magnetometru
* `amber-python-drivers`_ jest to projekt sterowników, napisanych w *python*, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:
 * **Roboclaw** - sterowanie silnikami robota
 * **Hokuyo** - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji o odległościach innych przeszkód od robota

Klienci
-------

* `amber-java-clients`_ - jest to projekt dostarczają klientów, napisanych w *Java*, używanych przez korzystających z robota, w ich własnych aplikacjach, obsługiwane są:
 * **Roboclaw**
 * **Hokuyo**
 * **Ninedof**
* `amber-python-clients`_ jest to projekt dostarczają klientów, napisanych w *python*, używanych przez korzystających z robota, w ich własnych aplikacjach, obsługiwane są:
 * **Roboclaw**
 * **Hokuyo**
 * **Ninedof**

Pliki wspólne
-------------

* `amber-common`_ jest to projekt zawierający część wspólną wyżej wymienionych projektów, którymi są:
 * pliki opisu *ProtoBuf*

.. _Amber: https://github.com/dev-amber
.. _sterownikami: ./drivers.html
.. _klientami: ./clients.html
.. _amber-main: https://github.com/dev-amber/amber-main
.. _amber-cpp-drivers: https://github.com/dev-amber/amber-cpp-drivers
.. _amber-python-drivers: https://github.com/dev-amber/amber-python-drivers
.. _amber-java-clients: https://github.com/dev-amber/amber-java-clients
.. _amber-python-clients: https://github.com/dev-amber/amber-python-clients
.. _amber-common: https://github.com/dev-amber/amber-common