Telemetry Services
==================

The collection of Telemetry Services are meant to provide the full history of vehicle telemetry transmitted by a device. This history is made available in three different formats across three separate, but similar API methods.

* Snapshots - Time-series history of one or more vehicle parameters
* Locations - Time-series of locations with corresponding vehicle parameters returned as valid GeoJSON
* Messages - Time-series of the raw, unfiltered messages from a device

Common across all three of these methods is the way in which the time-series data is accessed. These follow the "Stream Pagination" pattern described above and allow for pagination in time.

It's important to note that the pattern in which each parameter is reported is different and somewhat unpredictable depending on the type of vehicle or the vehicle's condition. There are a few parameters that we try to send as often as possible (RPM, Vehicle Speed, etc.), and location is sent with every message when available. There are also some parameters that never change for a vehicle such as Fuel Type or O2 Sensor Locations (boring stuff, right?). However, all parameters that are provided by a vehicle are reported at least once every minute or so after startup.

.. toctree::
  :maxdepth: 1

  device-messages
  location-history
  telemetry-snapshots