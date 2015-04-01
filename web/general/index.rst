Vinli General Platform
======================

The Vinli Web API provides access over HTTP/SSL to the data collected from the Vinli devices.  This set of tools provides two tiers of services for your applications to consume.  Tier 1 provides access and functionality around the "raw" data gathered from your customers' devices.  These include:

* Platform Services - provides the administrative actions for your application such as registering devices, setting up groups, getting vehicle information, and monitoring transactions
* Telemetry Services - provides access to time-series data for all vehicle telemetry gathered on a device-by-device basis
* Event Services - provides tools to create rules based on vehicle parameter limits or geofences and notifies your application when a device violates these rules

Tier 2 services provide a bit more analysis and "expertise" on top of the data provided by Tier 1.  These services include:

* Trip Services - automatically detects "trips" for a given device or vehicle and gives telemetry and other information on a trip-by-trip basis
* Diagnostic Services - provides access to detailed diagnostic information about a device (DTC Codes aka "Check Engine Light") including historical diagnostics
* Behavioral Services - provides "report cards" for given devices or vehicles based on the driver's behavior and other factors

All of the services above is accessed in a similar manner with respect to authentication, pagination, etc.  More detail about these standards is included in the following sections.

.. toctree::
   :maxdepth: 1

   authentication
   pagination
   dates
