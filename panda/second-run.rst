Drugie uruchomienie konfiguracyjne
----------------------------------

* **Zalogować** się do systemu poprzez SSH: ``ssh root@192.168.2.50``.
* **Ustawić** hasło dla użytkownika ``root`` przy pomocy ``passwd``.
* **Usunąć** linię ``apt-get install -y openssh-server`` z pliku ``/etc/rc.local``.
* **Ustawić** nazwę systemu w plikach:

``/etc/hostname``
::

    panda.robonet

``/etc/hosts``
::

    127.0.0.1 localhost
    127.0.1.1 panda panda.robonet

Następnie należy **przerwać** konfigurację płytki z wykorzystaniem kreatora, który działa na konsoli (dostępnej przy instalacji z wykorzystaniem monitora i klawiatury).

* **Wywołać** polecenie ``fuser -k /var/cache/debconf/config.dat`` do oporu.
* **Usunąć** pakiet ``oem-config`` (z wykorzystaniem ``aptitude``) oraz katalog ``/var/lib/oem-config``.
* **Zrestartować** system poprzez ``reboot``.
