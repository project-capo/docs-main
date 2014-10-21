Sterowniki
==========

Wspierane sterowniki
--------------------

* `amber-cpp-drivers`_ jest to projekt sterowników, napisanych w *C/C++*, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:

    * **Roboclaw** - sterowanie silnikami robota
    * **Ninedof** - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji z przyspieszeniomierza, żyroskopu oraz magnetometru

* `amber-python-drivers`_ jest to projekt sterowników, napisanych w *python*, które pozwalają na komunikację z urządzeniami umieszczonymi na robocie. Wspierane są:

    * **Hokuyo** - odczytywanie informacji z sensora umieszczonego na robocie, dostarczającego informacji o odległościach innych przeszkód od robota

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
* komunikującą się z urządzeniem podłączonym do robota
* komunikującą się z mediatorem poprzez potoki

Sterownik odpowiada za:

* ustawienie parametrów urządzenia
* współbieżny dostęp do urządzenia przez wiele klientów
* obserwowanie obecności klientów
* wysyłanie wiadomości dla klientów, którzy zarejestrowali się jako nasłuchujący
* odbieranie komunikatów, ich obsługę i odsyłanie wiadomości, jeśli to konieczne

Działanie
---------

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

Przykład
--------

Przykładem sterownika, który realizuje powyższe funkcjonalności jest `DummyDriver`_. Sterowniki korzystają z `części wspólnej`_.

.. _DummyDriver: https://github.com/project-capo/amber-python-drivers/blob/master/src/amber/dummy/dummy.py
.. _części wspólnej: https://github.com/project-capo/amber-python-drivers/blob/master/src/amber/common/amber_pipes.py
