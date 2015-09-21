Instalacja systemu
==================

Do przeprowadznia procesu instalacji systemu potrzebne są:

* karta SD, o pojemności minimum 8 GB
* czytnik kart SD w komputerze (w przypadku posługiwania się maszyną wirtualną, czytnik kart SD na USB)
* płyta główna *PandaBoard* z zasilaczem prądu stałego o napięciu 5 V i natężeniu ~ 2.5 A
* router sieciowy WiFi
* opcjonalnie monitor z wejściem HDMI oraz klawiatura na USB lub kabel komunikacji szeregowej RS-232 DE-9

.. warning::

    Zwróć uwagę na wersję płytki, która jest określona na etykiecie umieszczonej na spodzie płytki. Poniższa instrukcja opisuje instalację systemu na *PandaBoard* w wersji *ES Rev B3* oraz *ES Rev B2*.

.. note::

    Jeśli masz możliwość korzystania z portu szeregowego, to korzystaj z niego. Instalacja systemu będzie łatwiejsza w porównaniu do instalacji bez wykorzystania portu szeregowego.

Dodatkowo, wymagana jest znajomość, do wykonania poniższej instrukcji:

* używania zdalnej konsoli SSH i generowanie kluczy SSH z wykorzystaniem *Putty* (windows) lub *ssh* (linux)
* obsługi podstawowych poleceń w powłoce systemu linux, jakimi są polecenia ``cd``, ``ls``, etc.
* obsługi edytora tekstu, jak na przykład ``vim`` lub ``nano``
* obsługi menadżera pakietów systemu Ubuntu *aptitude*

Zakłada się, że wgranie systemu na kartę odbywa się z systemu linux. Modyfikowanie karty możliwe jest *tylko* z wykorzystaniem systemu linux. Modyfikowanie odbywać się może po zamontowaniu partycji systemowej, na której wykorzystywany jest *ext4* jako system plików.

.. toctree::

    install/install-system
    install/first-run
    install/prepare-to-configuration
    install/second-run
    install/update-system
    install/post-configuration
    install/more
