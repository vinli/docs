Device DTC  Service
~~~~~~~~~~~~~~~~~~~

Get the list of current DTC Codes for a Device
``````````````````````````````````````````````

Request
+++++++

.. code-block:: json

      GET https://diagnostics.vin.li/api/v1/devices/47fa348e-c3fa-4cad-8272-61940eae7748/dtc_codes
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "dtcCodes" : [
          {
            "code" : "P0135",
            "start" : "2014-09-06T03:09:34.957Z"
          },
          {
            "code" : "P0171",
            "start" : "2014-09-05T12:05:46.893Z"
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "total" : 5,
            "offset" : 0,
            "limit" : 100,
            "links" : {
              "first" : "https://diagnostics.vin.li/api/v1/devices/47fa348e-c3fa-4cad-8272-61940eae7748/dtc_codes?offset=0&limit=20",
              "last" : "https://diagnostics.vin.li/api/v1/devices/47fa348e-c3fa-4cad-8272-61940eae7748/dtc_codes?offset=0&limit=20"
            }
          }
        }
      }



Get a history of DTC Code Events for a Device
`````````````````````````````````````````````

The DTC History Service provides historical information for DTC codes for a given vehicle.  Each time a new DTC code is seen, it triggers a DTC Event.  These events either resolve when the DTC code is no longer seen or remain "open" until the code is resolved.

Request
+++++++

.. code-block:: json

      GET https://diagnostics.vin.li/api/v1/devices/47fa348e-c3fa-4cad-8272-61940eae7748/dtc_code_events
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "dtcCodeEvents" : [
          {
            "code" : "P0135",
            "start" : "2014-09-06T03:09:34.957Z",
            "state" : "open"
          },
          {
            "code" : "P0171",
            "start" : "2014-09-05T12:05:46.893Z",
            "resolved" : "2014-09-11T23:15:40.781Z",
            "state" : "resolved"
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "total" : 5,
            "offset" : 0,
            "limit" : 100,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/devices?offset=0&limit=20",
              "last" : "https://platform.vin.li/api/v1/devices?offset=0&limit=20"
            }
          }
        }
      }