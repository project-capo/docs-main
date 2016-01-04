Device types
============

Currently supported devices:

* **Ninedof** - read values from **motion sensor**: accelerometer, gyroscope, compass
* **Roboclaw** - managing **engines** and reading current speed of each engine
* **DriveSupport** - managing **engines** with support from laser scanner and motion sensor (depends on **Hokuyo** and **Ninedof**)
* **DriveToPoint** - moving robot from point to point as per provided list of points, additional information about environment is used like location and view of visible area (depends on **Roboclaw** or **DriveSupport** and **Location**)
* **Hokuyo** - used to read values about distance between robot and obstacles located around robot
* **Location** - provides information about approximate location of robot in closed area (depends on **Hokuyo** and **Roboclaw**)
* **Maestro** - managing controller for servo motors (eg. used in arm)
* **PidFollowTrajectory** - moving robot by following line (depends on **Roboclaw** or **DriveSupport** and **Location**)

Ninedof
-------

Main functions provided by this driver are following:

* *one-time read* data from accelerometer, gyroscope, compass
* *all-time read* data from sensors

It is possible to decide which data will be read from sensors. It is possible to set this for one-time and all-time operations.

Roboclaw
--------

Main function which can be done with engines are following:

* *set speed* for each engine
* *read current speed*  from engines encoders

Used unit for speed is ``mm/s``.

DriveSupport
------------

That driver provides identical operations as *Roboclaw* driver. Used client is the same as for *Roboclaw*.

DriveToPoint
------------

That driver allow to do following operations:

* set list of points which should be reached
* read list of points which were reached
* read last reached point
* read list of points which should be reached
* read point which should be reached as next

Hokuyo
------

Main functions which are provided by this device are following:

* *one-time read* data from scanner
* *all-time read* data from scanner

Scan is a set of data combined in tuples which are having angle and distance.

Scanner has a range of activity in which the distance is correctly measured. In our case it is between 50 ``mm`` and 5 ``m``. When the distance is higher than 5 ``m`` it is marked as ``zero``. When the distance is lower than 50 ``mm`` or close to ``zero`` it means that is *almost* zero and it should be treated as too close.

Location
--------

Main function of this driver is provinding information about location. That driver depends on *Hokuyo* and *Roboclaw* drivers.
