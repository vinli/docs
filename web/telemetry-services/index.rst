Telemetry Services
==================

Telemetry Services are meant to provide the full history of vehicle telemetry that has been transmitted by a device. This history is made available by three different methods across three separate but similar API methods.

The three telemetry methods are:

* Snapshots - Time-series history of one or more vehicle parameters
* Locations - Time-series of locations with corresponding vehicle parameters returned as valid GeoJSON
* Messages - Time-series of the raw, unfiltered messages from a device

The way in which time-series data is accessed is common across all three methods. They follow the "Stream Pagination" pattern described above, allowing for pagination in time.

.. note:: The pattern in which each parameter is reported is different and somewhat unpredictable, depending on the type of vehicle or the vehicle's condition. Parameters such as RPM, Vehicle Speed, etc. are sent as often as possible and the location is sent with every message when available. Parameters such as Fuel Type or O2 Sensor Locations will never change. However, all parameters that are provided by a vehicle are reported at least once every minute or so after startup.

.. toctree::
  :maxdepth: 1

  device-messages
  location-history
  telemetry-snapshots
