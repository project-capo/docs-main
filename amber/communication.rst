Communication
=============

Participants
------------

In communication participate:

* one mediator
* one or more client(s)
* one or more driver(s)

Mediator features:

* is responsible for routing messages between clients and drivers
* does not modify message which is known only for driver and client
* processes message headers:

    * updates information about clients
    * updates information about type and number of device

Protocol
--------

Driver communicates with mediator using pipes - standard input and output. It is required that driver will wait for data on standard input and will send data using standard output. Client communicates with mediator using UDP. Mediator is listening on port ``26233``.

Format of message used in communication with mediator:

* 2 bytes which contain information about header length
* header data
* 2 bytes which contain information about message length
* message data

Length value should be sent in ``big-endian`` format (used in network). Be aware if used data are ``signed`` or ``unsigned``. Due to fact that *Java* ``signed`` should be used.

Header and message data are binary data. Be aware how driver is communicating with mediator, what are the settings for pipes. For example in *python* interpreter should be started with option ``-u`` which allow using standard input and output in binary mode.

For serialization *Google Protobuf* is used. It is required that header will be combatible with used by mediator. Messages are not touched by mediator. It is recommended to use *protobuf* for message and to have message in format combatible with used in Amber project. Current header and message format is published in file `project-capo/amber-common/drivermsg.proto`_.

.. _project-capo/amber-common/drivermsg.proto: https://github.com/project-capo/amber-common/blob/master/proto/drivermsg.proto

Messages
--------

Messages sent between clients and drivers contain:

* header ``DriverHdr``

    * ``deviceType`` - device type
    * ``deviceID`` - device number
    * ``clientIDs`` - clients numbers

* message ``DriverMsg``

    * ``type``  - message type
    * ``synNum`` - request number, set by client
    * ``ackNum`` - reply number, set by driver
    * ``listenerNum`` - listener number
    * additional fields (``extensions``)

Current device types ``DeviceType``:

* 0 - unknown, not used
* 1 - **NineDof** (motion sensor)
* 2 - **Roboclaw** (engines)
* 3 - **Stargazer** (robot location based on markers)
* 4 - **Hokuyo** (laser scanner)
* 5 - **Dummy** (testing)
* 6 - **Location** (computed robot location)
* 7 - **Maestro** (servo-motors)
* 8 - **DriveToPoint** (following list of points)
* 9 - **CollisionAvoidance** (not used)
* 10 - **PidFollowTrajectory** (following line)

Current driver type messages ``DriverMsg``:

* **DATA** - data sent between clients and drivers
* **PING** - echo request sent by mediator, currently not used
* **PONG** - echo reply sent by driver or client, currently not used
* **CLIENT_DIED** - information sent by client when client was correctly closed
* **DRIVER_DIED** - information sent by driver when driver was correctly closed
* **SUBSCRIBE** - subcribe messages sent by client
* **UNSUBSCRIBE** - closing subscribtion
