Transaction Service
-------------------


### Get All Transactions for this Application

Returns a list of all transactions performed by this Application.

Results are returned in reverse-chronological order and use the "Stream Pagination" method.

#### Request


      GET https://platform.vin.li/api/v1/transactions
      Accept: application/json

#### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "transactions" : [
          {
            "id": "f7ef31e5-9db0-438c-9328-927f66ceab77",
            "timestamp": "2014-08-25T05:26:55.426Z",
            "path": "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType",
            "service": "telemetry",
            "statusCode": 200,
            "method": "GET",
            "deviceId": "27a2ac50-d7bd-11e3-9c1a-0800200c9a66"
          },
          ...
        ],
        "meta" : {
          pagination : {
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



