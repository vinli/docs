DTC Info Service
-----------------

Get Information About a DTC Code
```````````````````````````````````

There's a lot of information encoded in the DTC codes reported by a Vehicle.  This method is meant to provide this information for a given DTC code so that your Application can present useful information to the end-user.

Request
+++++++

::
	
      GET https://diagnostic.vin.li/api/v1/codes?number=P0001
      Accept: application/json

Response
++++++++

::
	
      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "codes": [
          {
            "id": "2db60bc5-0548-43ee-91c0-c34d59ce71ce",
            "make": "generic",
            "system": "powertrain",
            "subSystem": "Fuel and air metering",
            "number": "P0001",
            "description": "Fuel Volume Regulator Control Circuit/Open",
            "links": {
              "self": "http://diagnostic.vin.li/api/v1/codes/2db60bc5-0548-43ee-91c0-c34d59ce71ce"
            }
          }
        ],
        "meta": {
          "pagination": {
            "total": 1,
            "limit": 20,
            "offset": 0,
            "links": {
              "first": "http://172.17.0.18:80/api/v1/codes?offset=0&limit=20",
              "last": "http://172.17.0.18:80/api/v1/codes?offset=0&limit=20"
            }
          }
        }
      }
