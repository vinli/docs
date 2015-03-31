Service Service
--------------

### Get App Service Usage Stats

May include since and/or until dates to limit the time range of the usage statistics.

#### Request

      GET https://platform.vin.li/api/v1/services/usage
      Accept: application/json

#### Response


      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "services" : [
          {
            "name": "devices",
            "transactions": 1024
          },
          ...
        ]
      }
