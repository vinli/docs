Transaction Service
~~~~~~~~~~~~~~~~~~~

Get All Transactions for this Application
`````````````````````````````````````````

Returns a list of all transactions performed by this Application.

Results are returned in reverse-chronological order and use the "Stream Pagination" method.

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/transactions
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "transactions" : [
          {
            "id": "e7924989-e942-4ebb-a566-427984b91af1",
            "timestamp": "2015-06-22T00:30:19.455Z",
            "path": "/api/v1/devices?limit=1",
            "statusCode": 200,
            "method": "GET",
            "service": "vinli-platform-service"
          },
          {
            "id": "b7d746ce-1794-4796-9dc9-30ae091d1ce6",
            "timestamp": "2015-06-20T21:41:13.520Z",
            "path": "/api/v1/devices/c38ce5f2-0c4d-4d82-b301-fd87af5fcbd3/locations?limit=20",
            "service": "vinli-telemetry-service",
            "method": "GET",
            "statusCode": 200
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "remainingCount" : 1324,
            "limit" : 50,
            "until" : 1408945415426,
            "links" : {
              "latest" : "https://platform.vin.li/api/v1/transactions",
              "prior" : "https://platform.vin.li/api/v1/transactions?until=1408944636328"
            }
          }
        }
      }



