Internal Vehicle Service
========================


List All Vehicles
-----------------

### Request

      GET /api/v1/_internal/vehicles
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicles" : [
          {
            "id" : "89dd2000-d707-11e3-9c1a-0800200c9a66",
            "year" : "2007",
            "make" : "Toyota",
            "model" : "Camry",
            "trim" : "SE V6",
            "vin" : "2B4GP44R6WR941457",
            "infoUpdatedAt" : 13995913779934,
            "infoUpdatedStatus" : "success"
            "links" : {
              "self" : "/api/v1/vehicles/89dd2000-d707-11e3-9c1a-0800200c9a66"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            ...
          }
        }
      }


Get a Vehicle
-------------

### Request

      GET /api/v1/_internal/vehicles/89dd2000-d707-11e3-9c1a-0800200c9a66
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicle" : {
          "id" : "89dd2000-d707-11e3-9c1a-0800200c9a66",
          "year" : "2007",
          "make" : "Toyota",
          "model" : "Camry",
          "trim" : "SE V6",
          "vin" : "2B4GP44R6WR941457",
          "infoUpdatedAt" : 13995913779934,
          "infoUpdatedStatus" : "success",
          "metadata" : { ... }
          "links" : {
            "self" : "/api/v1/vehicles/89dd2000-d707-11e3-9c1a-0800200c9a66"
          }
        }
      }
