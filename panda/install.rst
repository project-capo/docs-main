Instalacja
==========

Do przeprowadznia procesu instalacji potrzebne jest:

* karta SD, minimum 8GB
* czytnik kart SD w komputerze
* płyta główna PandaBoard z zasilaczem prądu stałego 5V i natężeniu ~ 2.5A
* router z Access Point
* opcjonalnie monitor z wejściem HDMI oraz klawiatura na USB

.. warning::

    Zwróć uwagę na wersję płytki, która jest określona na etykiecie umieszczonej na spodzie płytki. *Ubuntu 12.02.5 LTS* działa poprawnie na płytkach ``rev A4``, ``ES rev B2``. *Ubuntu 14.04.1 LTS* działa poprawnie na płytkach ``rev A4``, ``ES rev B2``. Póki co nie jest możliwe uruchomienie wykonanej wg poniższej instrukcji karty na płytce oznaczonej jako ``ES rev B3``.

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
