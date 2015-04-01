Telemetry Messages Service
~~~~~~~~~~~~~~~~~~~~~~~~~~

Get a List of Telemetry Messages
````````````````````````````````

Returns the latest `limit` number of telemetry messages that occurred before or at the `until` time and after the `since` time. If the `until` time is not specified, then the service will return snapshots until the current time when the call is made.

These messages are sent at least every five seconds and include the latest value of parameters captured by the Vinli device since the last message sent.


Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages
      Accept: application/json

* `until` - Results will contain snapshots whose timestamps are less than or equal to the `until` value. If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain snapshots whose timestamps are greater than the `since` value. If an `since` value is not specified, no lower limit will be placed on the returned snapshots.
* `limit` - Results will contain no more than `limit` number of snapshots


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "messages" : [
          {
            "timestamp": "2014-07-14T17:46:06.759Z",
            "vehicleSpeed": 12,
            "calculatedLoadValue": 34.5,
            "fuelType": "Gasoline",
            "rpm": 1254,
            "location": {
              "longitude": -90.0811,
              "latitude": 29.9508
            }
          },
          {
            "timestamp": "2014-07-14T17:46:01.544Z",
            "vehicleSpeed": 15,
            "rpm": 1766,
            "location": {
              "longitude": -90.0813,
              "latitude": 29.950802
            }
          },
          {
            "timestamp": "2014-07-14T17:45:54.872Z",
            "vehicleSpeed": 16,
            "calculatedLoadValue": 56.3,
            "rpm": 1766,
            "location": {
              "longitude": -90.08104,
              "latitude": 29.950813
            }
          }
          ...
        ],
        "meta" : {
          "pagination" : {
            "remainingCount" : 1324,
            "limit" : 50,
            "until" : 1394733261450,
            "links" : {
              "latest" : "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages"
              "prior" : "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages?until=1394733251897"
            }
          }
        }
      }



Get a Specific Telemetry Message
````````````````````````````````

Returns a particular message by `messageId`. This is primarily used when a specific message is referenced by a different service.


Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages/2f11d630-141e-11e4-b717-5977b6c38d23
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message" : {
          "timestamp": "2014-07-14T17:46:06.759Z",
          "vehicleSpeed": 12,
          "calculatedLoadValue": 34.5,
          "fuelType": "Gasoline",
          "rpm": 1254,
          "location": {
            "longitude": -90.0811,
            "latitude": 29.9508
          }
        }
      }



