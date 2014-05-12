Typy urządzeń
=============

Obecnie obsługiwane są urządzenia:

* Ninedof - odczytywanie wartości z przyspieszeniomierza, żyroskopu, kompasu
* Roboclaw - sterowanie silnikami i odczytywanie aktualnej prędkości każdego silnika
* Hokuyo - odczytywanie wartości odległości od otoczenia z skanera laserowego

Ninedof
-------

Głównymi akcjami, które można wykonać przy pomocy czujnika są:

* odczytanie wartości z przyspieszeniomierza, żyroskopu, kompasu
* ciągłe odczytywanie danych z czujników

Możliwe jest określenie, które dane będą odczytywane z czujnika. Możliwe jest ustalenie tego przy pojedynczym odebraniu danych z czujnika, jak i w ciągłym trybie.

Roboclaw
--------

Głównymi akcjami, które można wykonać na silnikach są:

* ustawienie prędkości każdego z czterech silników
* odczytanie aktualnej prędkości z enkoderów z silników

Jednostką podawanych prędkości jest ``[mm/s]``.

Hokuyo
------

Głównymi akcjami, które można wykonać przy pomocy skanera laserowego są:

* jednorazowe odczytanie skanu otoczenia
* ciągłe odczytywanie skanów otoczenia

Skanem otoczenia jest zbiór danych, w których wartości kąta powiązane są wartościami odległości od otoczenia.

W przypadku odległości większej niż obsługiwana przez lasera (w przypadku Hokuyo: >5m), występuje wartości ``zero``. Przyjąć należy, że ``zero`` nie jest odległości zerową. Budowa lasera i układów mierzących odległość nie dopuszcza odległości zerowej. Możliwa jest wartość bliska zerowej odległości.

Dodatkowymi akcjami są odczytanie:

* wersji oprogramowania sensora
* stanu sensora
* specyfikacji sensora