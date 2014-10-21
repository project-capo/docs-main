Drugie uruchomienie konfiguracyjne
----------------------------------

* **Zalogować** się do systemu poprzez SSH: ``ssh root@192.168.2.50``.
* **Ustawić** hasło dla użytkownika ``root`` przy pomocy ``passwd root``. Domyślny hasłem dla roota w *Robolab* jest ``panda2013``.
* **Usunąć** linię ``apt-get install -y openssh-server`` z pliku ``/etc/rc.local``.
* **Ustawić** nazwę systemu w plikach:

``/etc/hostname``

.. code-block:: sh

    panda.robonet

``/etc/hosts``

.. code-block:: sh

    127.0.0.1 localhost
    127.0.1.1 panda panda.robonet

.. warning::

    Należy **przerwać** konfigurację płytki z wykorzystaniem kreatora, który działa na konsoli (dostępnej przy instalacji z wykorzystaniem monitora i klawiatury).

* **Wywołać** polecenie ``fuser -k /var/cache/debconf/config.dat`` do oporu.
* **Usunąć** pakiet ``oem-config`` (z wykorzystaniem ``aptitude`` - ``aptitude purge oem-config``) oraz katalog ``/var/lib/oem-config``.
* **Zrestartować** system poprzez ``reboot``.
