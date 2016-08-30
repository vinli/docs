Telemetry Services
==================

Telemetry Services provide time-series data from vehicle parameters and location. This history is available in three formats:

* **messages format** provides time-series of the raw, unfiltered messages from a device
* **locations format** returns time-series of locations with corresponding vehicle parameters returned as valid GeoJSON
* **telemetry snapshots** deliver time-series history of one or more vehicle parameters


All of these data formats are provided using `stream pagination`_.

The reported format of each parameter can be different depending on the type of vehicle or the vehicle's condition.

Some parameters change often, and others not at all. For example, Telemetry Service sends RPM, vehicle speed, etc. as often as possible, location with every message when available. However, Fuel Type or O2 Sensor Locations will never change.

In any case, all parameters that are provided by a vehicle are reported at least once every minute or so after startup.

.. _stream pagination: ../general/pagination.html#stream-pagination

.. toctree::
  :maxdepth: 2

  device-messages
  location-history
  telemetry-snapshots
  pids
