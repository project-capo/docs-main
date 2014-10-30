Klienci
=======

Wspierani klienci
-----------------

* `amber-java-clients`_ - jest to projekt dostarczają klientów, napisanych w *Java*, używanych przez korzystających z robota, w ich własnych aplikacjach, obsługiwane są:

    * **Ninedof**
    * **Roboclaw**
    * **Hokuyo**
    * **Location**
    * **Maestro**

* `amber-python-clients`_ jest to projekt dostarczają klientów, napisanych w *python*, używanych przez korzystających z robota, w ich własnych aplikacjach, obsługiwane są:

    * **Ninedof**
    * **Roboclaw**
    * **Hokuyo**

.. _amber-java-clients: https://github.com/project-capo/amber-java-clients
.. _amber-python-clients: https://github.com/project-capo/amber-python-clients

Poniżej znajdziemy opis korzystania z klientów oraz możliwości ich dalszego rozszerzania.

Cechy klienta
-------------

Klient jest:

* biblioteką wykorzystywaną w aplikacji
* dostarczającą możliwości komunikacji z danymi sterownikami
* komunikującą się z mediatorem przez sieć

Klient odpowiada za:

* zestawienie połączenia z mediatorem, opartym na UDP
* wysyłanie wiadomości do mediatora z odpowiednimi wartościami typu i numeru urządzenia
* obsługę wiadomości przychodzących od mediatora

Przykład
--------

Przykładem klienta, który realizuje powyższe funkcjonalności jest `DummyClient`_. Klienci korzystają z `części wspólnej`_.

.. _DummyClient: https://github.com/project-capo/amber-python-clients/blob/master/src/amber/dummy/dummy.py
.. _części wspólnej: https://github.com/project-capo/amber-python-clients/tree/master/src/amber/common
