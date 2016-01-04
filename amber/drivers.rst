Drivers
=======

Supported drivers
-----------------

* `amber-cpp-drivers`_ is a project which contains drivers written in *C/C++*. Supported drivers are following:

    * **Ninedof** - reading information from sensor located on robot which provides information about motion from sensors accelerometer, gyroscope and compass
    * **Roboclaw** - controlling engines
    * **Stargazer** - provides ability to localize robot using camera and markers
    * **Location** - software computed location based on information from *Roboclaw* and *Hokuyo*
    * **Maestro** - servo-motors used in arm

* `amber-python-drivers`_ is a project which contains drivers written in *python*. Supported drivers are following:

    * **Hokuyo** - reading information from scanner about environment
    * **DriveSupport** - used to control engines, additional data are used like scans and motion data
    * **DriveToPoint** - allow to drive the route by list of points
    * **Roboclaw** - used to control engines without any additional support

.. _amber-cpp-drivers: https://github.com/project-capo/amber-cpp-drivers
.. _amber-python-drivers: https://github.com/project-capo/amber-python-drivers

Mediator configuration
----------------------

Each driver has device type and number assigned. That values are set in `Amber configuration`_. Configuration sould be saved in file ``apps/amber/priv/settings.config``.

Example configuration::

    {supervised_driver,
      {driver,
        {driver_name}
      },
      {driver_type_number, driver_nummber},
      [
        {cdriver, "path/to/driver"},
        {config_file, "path/to/driver/configuration"},
        {log_config_file, "path/to/log/configuration"}
      ]
    }.

Paths to configuration are not required. Required is path to executable file used to start the driver.

.. _Amber configuration: https://github.com/project-capo/amber-erlang-mediator/blob/master/apps/amber/priv/settings.config.example

Driver features
---------------

Driver is:

* an application which is running on robot
* an app. which is communicating with device connect to robot
* an app. which is communicating with mediator using pipes

Driver is responsible for:

* setting device parameters
* supporting simultaneous and parallel access to device
* monitoring clients presence and activity
* sending messages to clients which are registered as subscribers for specific type of messages
* receiving messages, servicing that messages and replying if it is needed

How it work
-----------

.. warning::

   Following guidelines are as a consequence of common part in messages sent between clients and drivers. Using `DriverMsg`_ is not required. Message format can be manully definded, but so far drivers and clients does not support it.

Driver should support following features:

* handling received messages:

    * **DATA** - contains data which should be processed by driver
    * **PING** - echo request sent by mediator to check if driver is still alive, current not used, as a result driver should reply from **PONG**
    * **SUBSCRIBE** i **UNSUBSCRIBE** - used for client registration
    * **CLIENT_DIED** - used to inform driver about closed client, as a result client should be removed from subscribers list similar to **UNSUBSCRIBE**

Additionally it is recommended that driver should sent **DRIVER_DIED** to mediator when it is closing correctly.

Also driver should support:

* initialize device
* set device parameters
* buffer data from device
* synchronous access to device

.. _DriverMsg: https://github.com/project-capo/amber-common/blob/master/proto/drivermsg.proto

Example
--------

Example of driver can be `DummyDriver`_. Drivers use `common parts`_.

.. _DummyDriver: https://github.com/project-capo/amber-python-drivers/blob/master/src/amberdriver/dummy/dummy.py
.. _common parts: https://github.com/project-capo/amber-python-drivers/blob/master/src/amberdriver/common/amber_pipes.py
