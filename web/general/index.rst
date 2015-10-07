The Vinli Platform
==================

The Vinli Platform allows applications to get data from Vinli devices, using a fast, simple RESTful API. Applications can get both raw and synthesized data.

For raw data:

* **Platform Service** administers your application. You can manage devices, get vehicle information, and monitor transactions.
* **Telemetry Service** delivers time-series data.
* **Event Service** offers subscriptions for vehicle events and powerful, rule- based event notifications.
* **Rule Service** creates event subscriptions based on vehicle state or georeferences.

For synthesized data:

* **Trip Service** organizes and summarizes telemetry by vehicle ignition and shutdown.
* **Diagnostic Service** allows applications to discover the malfunction state of the vehicle and provides diagnostic trouble codes.
* **Behavioral Service** categorizes driver risk based on driver behavior, vehicle conditions, and geographical travel patterns.
* **Safety Service** provides collision history and telemetry details of collisions. This service is often used together with an Event Service subscription to *collision* events.

Vinli Platform services authenticate your application and let you configure pagination. Vinli applications must authenticate themselves and their user’s actions. Pagination can affect the format of dates and times.

Get the details in these sections:

.. toctree::
   :maxdepth: 2

   authentication
   dev-device
   pagination
   dates
