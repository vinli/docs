Telemetry Messages
-------------------

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
* `since` - Results will contain snapshots whose timestamps are greater than the `since` value. If a `since` value is not specified, no lower limit will be placed on the returned snapshots.
* `limit` - Results will contain no more than `limit` number of snapshots


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "messages" : [
           {
            "id": "c5c55c92-59ae-440d-881e-24f6b287ac32",
            "timestamp": "2016-12-19T14:21:45.846Z",
            "data": {
              "location": {
                "type": "Point",
                "coordinates": [
                  -96.790123,
                  32.782034
                ]
              },
              "accel": {
                "maxZ": -5.707806,
                "maxX": -0.344767,
                "maxY": -7.240103,
                "minX": -0.651226,
                "minY": -7.27841,
                "minZ": -7.316718
              },
              "designOBDRequirements": "OBD-II as defined by the CARB",
              "rpm": 940,
              "vehicleSpeed": 16,
              "intakeManifoldPressure": 32,
              "calculatedLoadValue": 29.019607843137255,
              "massAirFlow": 4.49
            },
            "links": {
              "self": "https://telemetry.vin.li/api/v1/messages/c5c55c92-59ae-440d-881e-24f6b287ac32?deviceId=27a2ac50-d7bd-11e3-9c1a-0800200c9a66"
            }
          },
          {
            "id": "8bc21558-0ec5-4a77-b82e-e6a23c95675c",
            "timestamp": "2016-12-19T14:21:45.000Z",
            "data": {
              "location": {
                "type": "Point",
                "coordinates": [
                  -96.790127,
                  32.782054
                ]
              },
              "accel": {
                "maxZ": -5.286424,
                "maxX": -0.651226,
                "maxY": -7.393332,
                "minX": -1.072608,
                "minY": -7.43164,
                "minZ": -7.661484
              },
              "rpm": 1027,
              "oxygenSensorVoltage1b": 0.69,
              "shortTermFuelTrim1b": 0,
              "vehicleSpeed": 15,
              "intakeManifoldPressure": 39,
              "calculatedLoadValue": 34.509803921568626,
              "massAirFlow": 5.76
            },
            "links": {
              "self": "https://telemetry.vin.li/api/v1/messages/8bc21558-0ec5-4a77-b82e-e6a23c95675c?deviceId=27a2ac50-d7bd-11e3-9c1a-0800200c9a66"
            }
          },
          {
            "id": "fa23ac3c-9987-46ee-8969-bedaabd7819f",
            "timestamp": "2016-12-19T14:21:44.069Z",
            "data": {
              "location": {
                "type": "Point",
                "coordinates": [
                  -96.790113,
                  32.782085
                ]
              },
              "accel": {
                "maxZ": -6.24411,
                "maxX": -0.727841,
                "maxY": -6.971951,
                "minX": -1.608912,
                "minY": -7.27841,
                "minZ": -7.316718
              },
              "rpm": 902,
              "oxygenSensorLocations": [
                "Bank 1 Sensor 1",
                "Bank 1 Sensor 2"
              ],
              "vehicleSpeed": 15,
              "intakeManifoldPressure": 40
            },
            "links": {
              "self": "https://telemetry.vin.li/api/v1/messages/fa23ac3c-9987-46ee-8969-bedaabd7819f?deviceId=27a2ac50-d7bd-11e3-9c1a-0800200c9a66"
            }
          },
          {
            "id": "3297440a-b839-41a8-9559-75e308a6e384",
            "timestamp": "2016-12-19T14:21:43.210Z",
            "data": {
              "location": {
                "type": "Point",
                "coordinates": [
                  -96.790111,
                  32.782127
                ]
              },
              "accel": {
                "maxZ": -6.703799,
                "maxX": -0.612919,
                "maxY": -6.397339,
                "minX": -0.612919,
                "minY": -7.58487,
                "minZ": -6.742106
              },
              "calculatedLoadValue": 36.86274509803921,
              "massAirFlow": 6.1,
              "rpm": 888,
              "absoluteThrottleSensorPosition": 13.72549019607843
            },
            "links": {
              "self": "https://telemetry.vin.li/api/v1/messages/3297440a-b839-41a8-9559-75e308a6e384?deviceId=27a2ac50-d7bd-11e3-9c1a-0800200c9a66"
            }
          },
        ],
        "meta": {
          "pagination": {
            "remaining": 709,
            "until": "2016-12-19T19:53:39.244Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 4,
            "sortDir": "desc",
            "links": {
              "prior": "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages?limit=5&until=1461943861926"
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

      GET https://telemetry.vin.li/api/v1/messages/2f11d630-141e-11e4-b717-5977b6c38d23
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message" : {
          "id" : "27a2ac50-d7bd-11e3-9c1a-0800200c9a66",
          "timestamp": "2014-07-14T17:46:06.759Z",
          "data": {
            "location": {
              "type": "point",
              "coordinates": [
                -90.0811,
                29.9508
              ]
            },
            "vehicleSpeed": 0
          },
          "links" : {
            self": "https://telemetry.vin.li/api/v1/messages/2f11d630-141e-11e4-b717-5977b6c38d23"
          }
        }
      }



