Klienci
=======

Poniżej znajdziemy opis korzystania z klientów oraz możliwości ich dalszego rozszerzania.

Klient jest:

* biblioteką wykorzystywaną w aplikacji
* dostarczającą możliwości komunikacji z danymi sterownikami
* komunikującą się z mediatorem przez sieć

Klient odpowiada za:

* zestawienie połączenia z mediatorem, opartym na UDP
* wysyłanie wiadomości do mediatora z odpowiednimi wartościami typu i numeru urządzenia
* obsługę wiadomości przychodzących od mediatora

Przykładem klienta, który realizuje powyższe funkcjonalności jest `DummyClient`_. Klienci korzystają z `części wspólnej`_.

.. _DummyClient: https://github.com/dev-amber/amber-python-clients/blob/master/src/amber/dummy/dummy.py
.. _części wspólnej: https://github.com/dev-amber/amber-python-clients/tree/master/src/amber/common