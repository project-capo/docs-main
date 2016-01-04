Clients
=======

Supported clients
-----------------

* `amber-java-clients`_ - it is a project which contains clients written in *Java*. Following devices are supported:

    * **Ninedof**
    * **Roboclaw**
    * **Hokuyo**
    * **Location**
    * **Maestro**
    * **DriveToPoint**

* `amber-python-clients`_ - it is a project which contains clients written in *python*. Following devices are supported:

    * **Ninedof**
    * **Roboclaw**
    * **Hokuyo**
    * **Location**
    * **DriveToPoint**

.. _amber-java-clients: https://github.com/project-capo/amber-java-clients
.. _amber-python-clients: https://github.com/project-capo/amber-python-clients

Client features
---------------

Client:

* is library used in client application
* provides ability to communicate with devices located on robot
* communicates with mediator over network

Client is responsible for:

* setting connection with mediator over UDP
* sending messages to mediator with correct type and number of device
* handling messages which are coming from mediator

Example
-------

Example of driver can be `DummyClient`_. Drivers use `common parts`_.

.. _DummyClient: https://github.com/project-capo/amber-python-clients/blob/master/src/amberclient/dummy/dummy.py
.. _common parts: https://github.com/project-capo/amber-python-clients/tree/master/src/amberclient/common
