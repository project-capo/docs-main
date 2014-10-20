Komunikacja
===========

Uczestnicy
----------

W komunikacji uczestniczą:

* jeden mediator
* jeden klient lub wielu klientów
* jeden sterownik lub wiele sterowników

Cechy mediatora:

* odpowiada za przekazywanie komunikatów pomiędzy określonymi klientami i sterownikami
* nie ingeruje w wiadomości, jakie są znane tylko sterownikom oraz klientom
* obsługuje i przetwarza nagłówki wiadomości, w których

    * uzupełnia informacje o numerach klientów
    * wykorzystuje informacje o typie i numerze sterownika


Komunikacja i protokół
----------------------

Sterownik komunikuje się z mediatorem przy pomocy potoków. Są to potoki standardowego wyjścia i wejścia. Wymagane jest, by sterownik na standardowym wejściu oczekiwał na dane, a na standardowe wyjście umieszczał dane.

Klient komunikuje się z mediatorem przy pomocy połączenia sieciowego, UDP. Mediator nasłuchuje na dostępnych interfejsach systemu, na porcie ``26233``.

Protokół komunikacji z mediatorem jest następujący:

* 2 bajty długości nagłówka wiadomości
* nagłówek wiadomości o zadanej długości
* 2 bajty długości wiadomości
* wiadomość o zadanej długości

Wartość długości powinna być przesyłana w porządku ``big-endian``, zgodna z sieciowymi warunkami przesyłania danych. Należy zwrócić uwagę na to, czyli wartości są ``singed`` czy ``unsigned``. Ze względu na wykorzystywanie języka *Java*, przyjmuje się, że wartości bajtów są ``signed``.

Nagłówek oraz wiadomość są binarnymi ciągami znaków. Należy zwrócić uwagę na sposób komunikacji z mediatorem poprzez potoki. W przypadku używania języka *python*, należy ustawić działanie interpretera na binarne obsługiwanie wejścia i wyjścia. Możliwe jest to dzięki opcji ``-u``.

Do serializacji i deserializacji wykorzystywane jest *Google Protobuf*. Wymagane jest, by co najmniej nagłówek był zgodny z przyjętym w mediatorze. Wiadomości przesyłane przez mediator nie są sprawdzane i może to być dowolny ciąg znaków. Zaleca się, by to było zgodne z protobuf i postacią wiadomości przyjętą w projekcie.

Aktualna postać nagłówka i podstawowej wiadomości dostępna jest `project-capo/amber-common/drivermsg.proto`_.

.. _project-capo/amber-common/drivermsg.proto: https://github.com/project-capo/amber-common/blob/master/proto/drivermsg.proto

Komunikaty
----------

Wiadomości przesyłane między klientami a sterownikami składają się z:

* nagłówka ``DriverHdr``

    * ``deviceType`` - typie urządzenia
    * ``deviceID`` - numerze urządzenia
    * ``clientIDs`` - numerach klientów, którzy wysłali dany komunikat do sterownika

* wiadomości ``DriverMsg``

    * ``type`` - typie wiadomości
    * ``synNum`` - numerze zapytania, nadanym przez klienta
    * ``ackNum`` - numerze odpowiedzi, nadanym przez sterownik, odpowiadającym numerowi ``synNum``
    * ``listenerNum`` - numerze określający listener
    * dodatkowych pól (``extensions``)

Obecna numeracja typów sterowników ``DeviceType``:

* 0 - nieznany, nieużywany
* 1 - **NineDof** (czujnik ruchu)
* 2 - **Roboclaw** (silniki)
* 3 - nieużywany (dawniej Stargazer)
* 4 - **Hokuyo** (laser)
* 5 - **Dummy** (testowy)

Obecne typy wiadomości ``DriverMsg``:

* **DATA** - dane przesyłane i rozumiane przez sterownik i klienta
* **PING** - zapytanie mediatora o działanie sterownika czy klienta, obecnie nieużywane
* **PONG** - odpowiedź sterownika czy klienta, obecnie nie wymagana
* **CLIENT_DIED** - komunikat wysyłany przez klienta, przy poprawnym zamknięciu klienta
* **DRIVER_DIED** - komunikat wysyłany przez sterownik, przy poprawnym zamknięciu sterownika
* **SUBSCRIBE** - subskrypcja klienta nasłuchującego wiadomości
* **UNSUBSCRIBE** - zakończenie subskrypcji klienta
