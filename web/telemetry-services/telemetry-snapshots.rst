Telemetry Snapshots
~~~~~~~~~~~~~~~~~~~

Returns the latest `limit` number of telemetry snapshots that contain at least one of the requested parameters that occurred before or at the `until` time and after the `since` time. If the `until` time is not specified, then the service will return snapshots until the current time when the call is made.

Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType
      Accept: application/json

* `fields` - Comma-separated list of parameter keys to filter by
* `until` - Results will contain snapshots whose timestamps are less than or equal to the `until` value.  If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain snapshots whose timestamps are greater than the `since` value.  If a `since` value is not specified, no lower limit will be placed on the returned snapshots.
* `limit` - Results will contain no more than `limit` number of snapshots

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "snapshots": [
              {
                  "timestamp": 1394733260050,
                  "data": {
                      "vehicleSpeed": 12,
                      "calculatedLoadValue": 34.5,
                      "fuelType": "Gasoline"
                  }
              },
              {
                  "timestamp": 1394733255337,
                  "data": {
                      "vehicleSpeed": 15
                  }
              },
              {
                  "timestamp": 1394733251898,
                  "data": {
                      "rpm": 3827,
                      "calculatedLoadValue": 56.3
                  }
              }
          ],
          "meta": {
              "pagination": {
                  "remainingCount": 1324,
                  "limit": 50,
                  "until": 1394733261450,
                  "links": {
                      "latest": "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType",
                      "prior": "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType&until=1394733251897"
                  }
              }
          }
      }

