Uruchomienie
============

Mediator z sterownikami
-----------------------

Opis poniższy opisuje jak rozpocząć pracę z systemem w trybie natychmiastowym.

W celu uruchomienia środowiska, należy zainstalować:

* Erlang OTP
* Python z Virtualenv oraz Pip
* g++ z libboost-dev

Następnie:

* sklonować ``dev-amber/amber-cpp-drivers``
 * wykonać ``make all``
* sklonować ``dev-amber/amber-python-drivers``
 * wykonać ``sudo python setup.py install``
* sklonować ``dev-amber/amber-main``
 * wykonać ``make all``

Skopiować ``amber-main/apps/amber/priv/settings.config.example`` do ``amber-main/apps/amber/priv/settings.config`` z poprawkami (wystarczy usunąć znaki komentarza).

Uruchomić skrypt ``amber-main/start_amber.sh``. Aby zakończyć pracę mediatora, należy wywołać polecenie ``killall heart``. Logi aplikacji znajdują się w ``amber-main/log``.

Możliwe jest uruchomienie w trybie deweloperskim. Jest to standardowe uruchomienie mediatora, z włączonymi przeglądaniem logów oraz zamknięciem mediatora, po przerwaniu przeglądania logów ``[Ctrl]+[c]``.