Telemetry Snapshots
--------------------

Returns the latest `limit` number of telemetry snapshots that contain at least one of the requested parameters that occurred before or at the `until` time and after the `since` time. If the `until` time is not specified, then the service will return snapshots until the current time when the call is made.

Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=vehicleSpeed,rpm
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
            "id": "090442e2-6c04-3473-bf15-549622329c79",
            "timestamp": "2016-12-19T23:05:43.074Z",
            "data": {
                "vehicleSpeed": 12,
                "rpm": 850
            },
            "links": {
                "self": "https://telemetry.vin.li/api/v1/messages/090442e2-6c04-3473-bf15-549622329c79"
                }
            },
            {
            "id": "b8664969-dfba-4536-b610-1cdc2657d8b2",
            "timestamp": "2016-12-19T23:05:42.198Z",
            "data": {
                "rpm": 1805
            },
            "links": {
                "self": "https://telemetry.vin.li/api/v1/messages/b8664969-dfba-4536-b610-1cdc2657d8b2"
                }   
            },
            {
            "id": "89c4d874-cde5-4e7c-b7b4-59ce18d892d3",
            "timestamp": "2016-12-19T23:05:41.268Z",
            "data": {
                "vehicleSpeed": 19,
                "rpm": 1768
            },
            "links": {
                "self": "https://telemetry.vin.li/api/v1/messages/89c4d874-cde5-4e7c-b7b4-59ce18d892d3"
                }
            }
        ],
        "meta": {
            "pagination": {
            "remaining": 797812,
            "until": "2016-12-20T00:11:10.993Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 3,
            "sortDir": "desc",
            "links": {
                "prior": "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=vehicleSpeed,rpm"
                }  
            }
        }
    }
