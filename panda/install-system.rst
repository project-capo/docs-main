Instalacja systemu na karcie
----------------------------

* **Pobrać** obraz `Ubuntu Server 12.04 amrhf+omap4`_ dla PandaBoard z strony `Ubuntu`_. Więcej informacji na temat wsparcia Ubuntu dla płyt opartych o OMAP dostępne jest na stronie `ARM/OMAP`_.
* **Sprawdzić** sumy kontroler md5 z dostępnymi na `serwerze`_.
* **Sprawdź** czy karta SD jest w trybie *do zapisu*. Przełącznik powinien być przesunięty do góry, gdzie u góry karty znajdują są styki.
* **Umieścić** kartę w czytniku kart komputera.
* **Wywołać** jedno z poniższych poleceń:
::

    gunzip -c ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz | sudo dd bs=1M of=/dev/<device name>
    sync

lub:
::

    sudo sh -c 'zcat ubuntu-12.04-preinstalled-server-armhf+omap4.img.gz > /dev/<device name>'
    sync

* **Wyciągnąć** kartę z czytnika kart komputera.
* **Umieścić** kartę w czytniku kart *PandaBoard*.
* **Uruchomić** *PandaBoard* wykorzystując oryginalny zasilacz prądu stałego 5V i natężeniu ~ 2.5A.
