The Vinli Platform
==================

The Vinli Web API provides access over HTTP/SSL to the data collected from the Vinli devices.  This set of tools provides two tiers of services for your applications to consume.  Tier 1 provides access and functionality around the "raw" data gathered from your customers' devices.  These include:

* Platform Service - provides the administrative actions for your application such as maanging devices, getting vehicle information, and monitoring transactions
* Telemetry Service - provides access to time-series data for all vehicle telemetry gathered on a device-by-device basis
* Event Service - provides access to vehicle events as well as the ability to create subscriptions to these events
* Rule Service - provides tools to create rules based on vehicle parameter limits or geofences

Tier 2 services provide a bit more analysis and "expertise" on top of the data provided by Tier 1.  These services include:

* Trip Service - automatically detects "trips" for a given device or vehicle and gives telemetry and other information on a trip-by-trip basis
* Diagnostic Service - provides access to detailed diagnostic information about a device (DTC Codes aka "Check Engine Light") including historical diagnostics
* Behavioral Service - provides "report cards" for given devices or vehicles based on the driver's behavior and other factors
* Safety Service - provides access to collision history and collected safety information

All of the services above is accessed in a similar manner with respect to authentication, pagination, etc.  More detail about these standards is included in the following sections.

.. toctree::
   :maxdepth: 2

   authentication
   pagination
   dates
