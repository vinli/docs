Vinli Services Documentation
=============================

Overview
--------

Vinli is a platform for easily and quickly building connected car apps. Apps get vehicle data through Vinli services.

Tier 1, raw data services:
````````````````````````````

* `Platform Service`_ manages devices, gets vehicle information, and monitors transactions.

* `Telemetry Service`_ delivers time-series vehicle data.

* `Event Service`_ delivers vehicle events and offers powerful, rule-based event notifications.

* `Diagnostic Service`_ reveals the malfunction state of the vehicle and provides diagnostic trouble codes.

* `Distance Service`_ estimates the car odometer reading at a point in time and milage travelled in a time interval.


Tier 2, structured data services:
`````````````````````````````````

* `Trip Service`_ organizes and summarizes telemetry by vehicle ignition and shutdown.

* `Behavioral Service`_ categorizes driver risk based on behavior, vehicle conditions, and geographical travel patterns. It assigns a risk score.

* `Safety Service`_ provides history and telemetry details of collisions.

* `Rule Service`_ creates event subscriptions based on vehicle state or geofences.


Testing and Prototyping
````````````````````````

You can quickly prototype an app using `Virtual Vinli`_.

* select a `Virtual Vinli Route`_

* get data from a `Virtual Vinli Run`_ of the route

* use the returned virtual data to test your ideas


.. _Platform Service: web/platform-services/index.html
.. _Telemetry Service: web/telemetry-services/index.html
.. _Event Service: web/event-services/index.html
.. _Diagnostic Service: web/diagnostic-services/index.html
.. _Trip Service: web/trip-services/index.html
.. _Behavioral Service: web/behavioral-services/index.html
.. _Safety Service: web/safety-services/index.html
.. _Rule Service: web/rule-services/index.html
.. _API Reference: web/API-reference/index.html
.. _Distance Service: web/distance-services/index.html
.. _Virtual Vinli: web/virtual-vinli/index.html
.. _Virtual Vinli Route: web/virtual-vinli/routes.html
.. _Virtual Vinli Run: web/virtual-vinli/runs.html


Contents
--------

.. toctree::
   :maxdepth: 3

   web/general/index

.. toctree::
   :maxdepth: 3

   web/platform-services/index

.. toctree::
   :maxdepth: 3

   web/telemetry-services/index

.. toctree::
  :maxdepth: 3

  web/event-services/index

.. toctree::
  :maxdepth: 3

  web/rule-services/index

.. toctree::
  :maxdepth: 3

  web/diagnostic-services/index

.. toctree::
  :maxdepth: 3

  web/distance-services/index

.. toctree::
  :maxdepth: 3

  web/trip-services/index

.. toctree::
  :maxdepth: 3

  web/behavioral-services/index

.. toctree::
   :maxdepth: 3

   web/safety-services/index

.. toctree::
   :maxdepth: 3

   web/API-reference/index

.. toctree::
   :maxdepth: 3

   web/virtual-vinli/index


