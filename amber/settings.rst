Ustawienia
==========

Mediator
--------

Do uruchomienia mediatora, potrzeba skonfigurować sterowniki, które będą uruchomiane wraz z mediatorem. `Przykładową konfigurację`_ należy zaadaptować do swoich warunków i zapisać jako ``apps/amber/priv/settings.config``.

.. note::

    Obecnie w pełni wspierane sterowniki są *Roboclaw*, *Hokuyo* oraz *Location*. Te należy odkomentować z pliku konfiguracyjnego mediatora znadującego się w ``apps/amber/priv/settings.config``.

.. _Przykładową konfigurację: https://github.com/project-capo/amber-erlang-mediator/blob/master/apps/amber/priv/settings.config.example

Sterowniki
----------

Sterownikami i ich konfiguracją zarządzają ich twórcy. Dostarczana jest wraz z sterownikami.

Klienci
-------

Klientami i ich konfiguracją zarządzają ich twórcy. Dostarczana jest wraz z klientami.
