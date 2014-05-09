Zaczynamy
=========

Opis poniższy opisuje jak rozpocząć pracę z systemem w trybie natychmiastowym.

Na obrazie świeżym (czysty, pure, raw, original, galancie) systemie (taki zalecam, polecam, rekomenduję, proponuję) wystarczy:

* zainstalować erlanga (nawet z paczek)
* zainstalować git'a
* zainstalować python'a i pip'a
* zainstalować g++ z libboost-dev

Następnie:

* sklonować ``dev-amber/amber-cpp-drivers``
 * wykonać ``make all``
* sklonować ``dev-amber/amber-python-drivers``
 * wykonać ``sudo python setup.py install``
* sklonować ``dev-amber/amber-main``
 * wykonać ``make all``

Skopiować ``amber-main/apps/amber/priv/settings.config.example`` do ``amber-main/apps/amber/priv/settings.config`` z poprawkami (wystarczy odkomentować).

I odpalić skrypt ``amber-main/start_amber.sh``.