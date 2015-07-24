Device DTC  Service
~~~~~~~~~~~~~~~~~~~

Get the list of all DTC Codes for a Device
``````````````````````````````````````````

The DTC History Service provides historical information for DTC codes for a given vehicle.  Each time a new DTC code is seen, it triggers a DTC Event.  These events either resolve when the DTC code is no longer seen or remain "open" until the code is resolved.

Request
+++++++

.. code-block:: json

      GET https://diagnostics.vin.li/api/v1/vehicles/47fa348e-c3fa-4cad-8272-61940eae7748/codes
      Accept: application/json

The state query param may be used to filter the response. Valid values are active and inactive. These will filter the response to only include either DTC codes that are still on presently or not. The absence of the state query param will not filter the response and so the response will contain the full history DTC codes.

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "codes" : [
          {
            "id" : "86273a41-2d5a-427b-bfb8-474b73bace14",
            "deviceId" : "bc6825db-716a-47ae-9eb1-8752af83361d",
            "vehicleId" : "2594b0b5-0d9f-463a-b4e6-4eadc20bec49",
            "number" : "P0152",
            "start" : "2014-09-06T03:09:34.957Z",
            "stop" : null,
            "links" : {
              "device" : "https://platform.vin.li/api/v1/devices/bc6825db-716a-47ae-9eb1-8752af83361d",
              "vehicle" : "https://platform.vin.li/api/v1/devices/2594b0b5-0d9f-463a-b4e6-4eadc20bec49"
            }
          },
          {
            "id" : "b943019b-b0ab-4350-9595-5c09f79f18ed",
            "deviceId" : "bc6825db-716a-47ae-9eb1-8752af83361d",
            "vehicleId" : "2594b0b5-0d9f-463a-b4e6-4eadc20bec49",
            "number" : "P0135",
            "start" : "2014-09-06T03:09:34.957Z",
            "stop" : "2014-09-06T03:10:14.384Z",
            "links" : {
              "device" : "https://platform.vin.li/api/v1/devices/bc6825db-716a-47ae-9eb1-8752af83361d",
              "vehicle" : "https://platform.vin.li/api/v1/devices/2594b0b5-0d9f-463a-b4e6-4eadc20bec49"
            }
          },
          {
            "id": "429d0c42-381b-499c-bd6c-4a5620e6b1ed",
            "deviceId": "bc6825db-716a-47ae-9eb1-8752af83361d",
            "vehicleId": "2594b0b5-0d9f-463a-b4e6-4eadc20bec49",
            "number" : "P0171",
            "start" : "2014-09-05T12:05:46.893Z",
            "stop" : "2014-09-06T03:10:14.384Z",
            "links" : {
              "device" : "https://platform.vin.li/api/v1/devices/bc6825db-716a-47ae-9eb1-8752af83361d",
              "vehicle" : "https://platform.vin.li/api/v1/devices/2594b0b5-0d9f-463a-b4e6-4eadc20bec49"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "total" : 5,
            "offset" : 0,
            "limit" : 100,
            "links" : {
              "first" : "https://diagnostics.vin.li/api/v1/vehicles/47fa348e-c3fa-4cad-8272-61940eae7748/codes?offset=0&limit=20",
              "last" : "https://diagnostics.vin.li/api/v1/vehicles/47fa348e-c3fa-4cad-8272-61940eae7748/codes?offset=0&limit=20"
            }
          }
        }
      }
