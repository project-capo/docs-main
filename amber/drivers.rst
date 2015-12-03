Sterowniki
==========

Wspierane sterowniki
--------------------

* `amber-cpp-drivers`_ jest to projekt sterowników, napisanych w *C/C++*, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:

    * **Ninedof** - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji z przyspieszeniomierza, żyroskopu oraz magnetometru
    * **Roboclaw** - sterowanie silnikami robota
    * **Stargazer** - obsługa lokalizacji w oparciu o kamerę oraz markery
    * **Location** - programowa obsługa lokalizacji z wykorzystaniem algorytmu cząstek i analizy trakcji
    * **Maestro** - servo-mechanizmy wykorzystywane w ramieniu

* `amber-python-drivers`_ jest to projekt sterowników, napisanych w *python*, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:

    * **Hokuyo** - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji o odległościach innych przeszkód od robota
    * **DriveSupport** - osbługa sterowania silnikami ze wsparciem skanera laserowego oraz czujnika ruchu
    * **DriveToPoint** - obsługa poruszania się według listy punktów
    * **Roboclaw** - obsługa sterowania silnikami

.. _amber-cpp-drivers: https://github.com/project-capo/amber-cpp-drivers
.. _amber-python-drivers: https://github.com/project-capo/amber-python-drivers

Konfiguracja z mediatorem
-------------------------

Sterownik posiada przypisany typ urządzenia oraz numer urządzenia. Wartości te ustawiane są w `konfiguracji Amber`_. Konfiguracja powinna być zapisana jako ``apps/amber/priv/settings.config``.

Konfiguracja jednego z sterowników::

    {supervised_driver,
      {driver,
        {nazwa_sterownika}
      },
      {numer_typu_sterownika, numer_sterownika},
      [
        {cdriver, "ścieżka/do/sterownika"},
        {config_file, "ścieżka/do/konfiguracji/sterownika"},
        {log_config_file, "ścieżka/do/konfiguracji/dziennika/sterownika"}
      ]
    }.

Ścieżki konfiguracji nie są wymagane, ważne jest podanie ścieżki do pliku wykonywalnego, który uruchomi sterownik.

.. _konfiguracji Amber: https://github.com/project-capo/amber-erlang-mediator/blob/master/apps/amber/priv/settings.config.example

Cechy sterownika
----------------

Sterownik jest:

* aplikacją uruchamianą na robocie
* app. komunikującą się z urządzeniem podłączonym do robota
* app. komunikującą się z mediatorem przez potoki powłoki systemu linux

Sterownik odpowiada za:

* ustawienie parametrów urządzenia
* wsparcie obsługi współbieżnego dostęp do urządzenia przez wiele klientów
* obserwowanie obecności klientów
* wysyłanie wiadomości dla klientów, którzy zarejestrowali się jako nasłuchujący na dany typ wiadomości
* odbieranie komunikatów, ich obsługę i odsyłanie wiadomości, jeśli to konieczne

Działanie
---------

.. warning::

   Poniższe zalecenia wynikają z postaci wspólnej wszystkich wiadomości przesyłanych między klientami a sterownikami. Stosowanie `DriverMsg`_ nie jest konieczne. Możliwe jest ustanowienie własnej postaci wiadomości, przy czym obecna postać sterowników i klientów nie wspiera własnej postaci wiadomości.

Sterownik powinien realizować funkcjonalności takie jak:

* obsługę odbierania wiadomość typów:

    * **DATA** - dane do przetworzenia przez sterownik, odebrane od klienta
    * **PING** - zapytanie o działanie, realizowane przez mediator, obecnie nie używane, odpowiedzią na zapytanie jest odesłanie wiadomości typu PONG
    * **SUBSCRIBE** i **UNSUBSCRIBE** - do rejestracji klienta nasłuchującego
    * **CLIENT_DIED** - zgłoszenie klienta o zakończeniu pracy, w przypadku, gdy dany klient był zarejestrowanych jako słuchacz, należy postąpić z nim podobnie, jak w przypadku **UNSUBSCRIBE**

Dodatkowo, co jest zalecane, sterownik powinien przy poprawnym zamykaniu się, wysłać do mediatora komunikat typu **DRIVER_DIED**.

Oprócz obsługi wiadomości, sterownik powinien realizować:

* inicjalizację pracy z urządzeniem
* ustawienie określonych parametrów pracy
* buforowanie danych z urządzenia
* współbieżny dostęp do urządzenia

.. _DriverMsg: https://github.com/project-capo/amber-common/blob/master/proto/drivermsg.proto

Przykład
--------

Przykładem sterownika, który realizuje powyższe funkcjonalności jest `DummyDriver`_. Sterowniki korzystają z `części wspólnej`_.

.. _DummyDriver: https://github.com/project-capo/amber-python-drivers/blob/master/src/amberdriver/dummy/dummy.py
.. _części wspólnej: https://github.com/project-capo/amber-python-drivers/blob/master/src/amberdriver/common/amber_pipes.py
