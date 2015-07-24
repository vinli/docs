Vinli Developer Documentation
===================================

.. Overview::

    Here you'll find the documentation of all the ways your applications can interact with the Vinli Platform and Device. Included are instructions for developing applications on the Web and mobile devices.

    Have any questions or find something we missed? Let us know by filing an issue on this repository.

    The documentation is split between each service of the Vinli Platform:

`General`_

`Platform Service`_
    The Platform Service offered allow access and control over devices, vehicles, and their relationships to your application in addition to some administrative access to transactions.

`Telemetry Service`_
    The collection of Telemetry Service are meant to provide the full history of vehicle telemetry transmitted by a device. This history is made available in three different formats across three separate, but similar API methods.

`Event Service`_
    The set of tools provided by Vinli's Event Service allows an application to create and manage complex sets of Rules that are evaluated on particular devices or groups of devices.

`Diagnostic Service`_
    In addition to transmitting real-time vehicle telemetry information, the Vinli Device interrogates the vehicle for the status of the malfunction indicator lamp (MIL) or "Check Engine Light". If the device detects that the MIL is illuniated, it requests the active diagnostic trouble codes (DTCs) for the vehicle. All of this inforamtion is sent to the Vinli Platform and can be accessed via the Diagnost Service API.

`Trip Service`_
    The Vinli device detects vehicle ignition and shutdown and sends those events to the platform. From these events, it is possible to organize the telemetry data into logical "Trips" for organizing users' activities in your application. The Trip Service provides access to a catalog of these Trips by Device or by Vehicle and provides mirrors of the Telemetry Service methods centered around these Trips.

    It's important to note that trips are sometimes created asyncrhonously--either because they have to be constructed by post-processing or after bulk data upload for a given device.

`Behavioral Service`_
    Based on long-term driving data, Vinli calculates and keeps track of behavioral statistics for particular devices and vehicles.

`Safety Service`_
    The Vinli Device is able to detect when a collision occurs based on internal sensor and select vehicle telemetry data. Using Vinli's Safety Service, your application can set up notification settings, list collision history, and retrieve detailed collision details.

.. _General: web/general/index.html
.. _Platform Service: web/platform-services/index.html
.. _Telemetry Service: web/telemetry-services/index.html
.. _Event Service: web/event-services/index.html
.. _Diagnostic Service: web/diagnostic-services/index.html
.. _Trip Service: web/trip-services/index.html
.. _Behavioral Service: web/behavioral-services/index.html
.. _Safety Service: web/safety-services/index.html

Find a bug, typo, or just want to make an improvement? This documentation is open source and available on `GitHub <https://github.com/vinli/docs/>`__. We like contributions!


Contents
--------

General
~~~~~~~~~~~~~~~~~

.. toctree::
   :maxdepth: 2

   web/general/index

Platform Service
~~~~~~~~~~~~~~~~~

.. toctree::
   :maxdepth: 2

   web/platform-services/index

Telemetry Service
~~~~~~~~~~~~~~~~~~

.. toctree::
   :maxdepth: 3

   web/telemetry-services/index

Event Service
~~~~~~~~~~~~~~

.. toctree::
  :maxdepth: 3

  web/event-services/index

Diagnostic Service
~~~~~~~~~~~~~~~~~~~

.. toctree::
  :maxdepth: 3

  web/diagnostic-services/index

Trip Service
~~~~~~~~~~~~~

.. toctree::
  :maxdepth: 3

  web/trip-services/index

Behavioral Service
~~~~~~~~~~~~~~~~~~~

.. toctree::
  :maxdepth: 3

  web/behavioral-services/index

Safety Service
~~~~~~~~~~~~~~~

.. toctree::
   :maxdepth: 2

   web/safety-services/index


