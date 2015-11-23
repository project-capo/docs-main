Wymagania
=========

Środowisko pracy
----------------

.. note::

    Zakłada się, że wgranie systemu na kartę odbywa się z poziomu systemu Linux. Modyfikowanie karty możliwe jest *tylko* z wykorzystaniem systemu Linux. Modyfikowanie odbywać się może po zamontowaniu partycji systemowej, na której wykorzystywany jest system plików ``ext4``.

.. note::

    Na potrzeby instalacji systemu na karcie, przygotowana została maszyna wirtualna *RoboLab*.

Wykorzystywane technologie i narzędzia
--------------------------------------

Do wykonania poniższej instrukcji wymagana jest znajomość:

* obsługi podstawowych poleceń w powłoce systemu Linux, jakimi są polecenia ``cd``, ``ls``, ``tar``, ``gz``, etc.
* obsługi edytora tekstu, jak na przykład ``vim`` czy ``nano``
* obsługi menadżera pakietów systemu Ubuntu ``aptitude`` lub ``apt-get``
* obsługi aplikacji używanej do komunikacji z *PandaBoard* z wykorzystaniem portu komunikacji szeregowej
* obsługi zdalnej konsoli SSH i generowania kluczy SSH z wykorzystaniem *Putty* (windows) lub ``ssh`` (Linux)

W celu przeprowadzenia procesu instalacji systemu potrzebne są:

* karta SD o pojemności minimum 8 GB
* czytnik kart SD
 * w przypadku posługiwania się maszyną wirtualną *Robolab* wymagany jest czytnik kart USB
* port szeregowy (instnieje możliwość instalacji bez użycia portu szeregowego)
 * w przypadku posługiwania się maszyną wirtualną *Robolab* wymagany jest konwenter USB portu szeregowego
* płyta główna *PandaBoard* z zasilaczem prądu stałego o napięciu 5 V i natężeniu ok. 2.5 A
* router sieciowy z WiFi
* monitor z wejściem HDMI oraz klawiatura na USB lub kabel komunikacji szeregowej RS-232 DE-9 (opcjonalnie)
* stosowne przewody do komunikacji sieciowej

.. warning::

    Zwróć uwagę na wersję *PandaBoard*, która jest opisana na etykiecie umieszczonej na spodzie płytki. Poniższa instrukcja opisuje instalację systemu na *PandaBoard* w wersji *ES Rev B2* oraz *ES Rev B3*.
