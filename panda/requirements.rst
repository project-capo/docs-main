Requirements
============

Working environment
----------------

.. note::

    It is assumed that writing OS on card is done from Linux system. Modifying files on card can be done *only* from Linux system. Modification should be done after mounting system partition which file system is ``ext4``.

.. note::

    For installation process, virtual machine *Robolab* has been prepared.

Used technologies and tools
---------------------------

To understand and execute following instruction you need to be familiar with following things:

* using basic Linux commands, eg. ``cd``, ``ls``, ``tar``, ``gz``, etc.
* using console text editore, eg. ``vim`` or ``nano``
* using package manager used in Ubuntu eg. ``aptitude`` or ``apt-get``
* using console serial port application used in communication with *PandaBoard* eg. ``minicom``
* using SSH remote console and generating SSH keys eg. *Putty* (windows) or ``ssh`` (Linux)

To follow the operating system installation process following things are required:

* SD card size 8 GB or bigger
* SD card reader
 * if you are using virtual machine *Robolab* you need to have USD card reader
* serial port (there is ability to install system without using serial port)
 * if you are using virtual machine *Robolab* required is USB serial port conventer
* board *PandaBoard* with power supply with DC voltage 5 V and current ca. 2.5 A
* WiFi network router
* display with HDMI input and keyboard on USB or serial port communication cable RS-232 DE-9 (optional)
* other required network cables

.. warning::

    Please check *PandaBoard* board version. You should find this on label which can be found at the bottom of board. Following instruction describes installation process on boards *ES Rev B2* and *ES Rev B3*.
