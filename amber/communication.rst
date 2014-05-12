Komunikacja
===========

Uczestnicy
----------

W komunikacji uczestniczą:

* jeden mediator
* klient lub wielu klientów
* sterownik lub wiele sterowników

Mediator odpowiada za przekazywanie komunikatów pomiędzy określonymi klientami i sterownikami. Nie ingeruje w wiadomości, jakie są znane tylko sterownikom oraz klientom. Obsługuje i przetwarza nagłówki wiadomości, w których uzupełnia informacje o numerach klientów i wykorzystuje informacje o typie i numerze sterownika, z którym się komunikuje.

Komunikaty
----------

Wiadomości przesyłane między klientami a sterownikami składają się z:

* nagłówka ``DriverHdr``, posiadający informację o
 * ``deviceType`` - typie urządzenia
 * ``deviceID`` - numerze urządzenia
 * ``clientIDs`` - numerach klientów, którzy wysłali dany komunikat do sterownika
* wiadomości ``DriverMsg``
 * ``type`` - typie wiadomości
 * ``synNum`` - numerze zapytania, nadanym przez klienta
 * ``ackNum`` - numerze odpowiedzi, nadanym przez sterownik, odpowiadającym numerowi ``synNum``
 * ``listenerNum`` - numerze określający listener
 * dodatkowych pól

Obecna numeracja typów sterowników ``DeviceType``:

* 0 - nieznany, nieużywany
* 1 - `NineDof`_ (czujnik ruchu)
* 2 - `Roboclaw`_ (silniki)
* 3 - nieużywany (dawniej Stargazer)
* 4 - `Hokuyo`_ (laser)
* 5 - `Dummy`_ (testowy)

.. _NineDof:
.. _Roboclaw:
.. _Hokuyo:
.. _Dummy:

Obecne typy wiadomości ``DriverMsg``:

* DATA
* PING
* PONG
* CLIENT_DIED
* DRIVER_DIED
* SUBSCRIBE
* UNSUBSCRIBE
