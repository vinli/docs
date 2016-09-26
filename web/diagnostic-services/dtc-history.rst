Working with DTC Codes
----------------------

Get a list of DTCs for a Vehicle
````````````````````````````````

This provides historical record of DTC codes for a given vehicle.  Each time a new DTC code is seen, it triggers a DTC Event.  These events either resolve when the DTC code is no longer seen or remain "open" until the code is resolved.

Request
+++++++
.. code-block:: json

      GET https://diagnostic.vin.li/api/v1/vehicles/47fa348e-c3fa-4cad-8272-61940eae7748/codes
      Accept: application/json


The state query param may be used to filter the response. Valid values are active and inactive. These will filter the response to only include either DTC codes that are still on presently or not. The absence of the state query param will not filter the response and so the response will contain the full history DTC codes.

Response
++++++++
.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "codes": [
          {
            "id": "dd46be07-24d0-48ad-be76-c459d35661ed",
            "deviceId": "397c302b-b083-4e5f-940b-15824b228e0b",
            "vehicleId": "7e94bdb6-7578-484d-99f5-37dec3e172b6",
            "number": "P0102",
            "description": "Mass or Volume Air Flow Sensor \"A\" Circuit Low",
            "start": "2015-12-01T19:58:58.279Z",
            "stop": null,
            "links": {
              "code": "http://diagnostic.vin.li/api/v1/codes/27268249-a716-402c-8550-7fc0d4ae6335",
              "device": "http://platform.vin.li/api/v1/devices/397c302b-b083-4e5f-940b-15824b228e0b",
              "vehicle": "http://platform.vin.li/api/v1/vehicles/7e94bdb6-7578-484d-99f5-37dec3e172b6"
            }
          },
          {
            "id": "02ad82a5-f6e6-4957-8f65-bc791d7399ae",
            "deviceId": "397c302b-b083-4e5f-940b-15824b228e0b",
            "vehicleId": "7e94bdb6-7578-484d-99f5-37dec3e172b6",
            "number": "P0101",
            "description": "Mass or Volume Air Flow Sensor \"A\" Circuit Range/Performance",
            "start": "2015-12-01T19:58:58.279Z",
            "stop": null,
            "links": {
              "code": "http://diagnostic.vin.li/api/v1/codes/a5cc128c-9a9b-487d-a6dd-375a9cc62dc4",
              "device": "http://platform.vin.li/api/v1/devices/397c302b-b083-4e5f-940b-15824b228e0b",
              "vehicle": "http://platform.vin.li/api/v1/vehicles/7e94bdb6-7578-484d-99f5-37dec3e172b6"
            }
          },
          {
            "id": "91e105ab-4f65-434e-8f41-088735299319",
            "deviceId": "397c302b-b083-4e5f-940b-15824b228e0b",
            "vehicleId": "7e94bdb6-7578-484d-99f5-37dec3e172b6",
            "number": "P0100",
            "description": "Mass or Volume Air Flow Sensor \"A\" Circuit",
            "start": "2015-12-01T19:58:58.279Z",
            "stop": null,
            "links": {
              "code": "http://diagnostic.vin.li/api/v1/codes/88853bda-e43e-4f60-bd72-8083ff02c85f",
              "device": "http://platform.vin.li/api/v1/devices/397c302b-b083-4e5f-940b-15824b228e0b",
              "vehicle": "http://platform.vin.li/api/v1/vehicles/7e94bdb6-7578-484d-99f5-37dec3e172b6"
            }
          }
        ],
        "meta": {
          "pagination": {
            "remaining": 0,
            "until": "2015-12-01T19:58:58.761Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 20,
            "sortDir": "desc",
            "links": {}
          }
        }
      }

Get a Specific DTC
``````````````````

This route returns a specific DTC occurrence.

Request
+++++++
.. code-block:: json

      GET https://diagnostic.vin.li/api/v1/codes/313cc7d7-1ad6-491k-9e02-a3f48e62984a


Response
++++++++
.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "code": {
          "id": "313cc7d7-1ad6-491k-9e02-a3f48e62984a",
          "make": "generic",
          "system": "powertrain",
          "subSystem": "Ignition system or misfire",
          "twoByte": {
            "number": "P0301",
            "description": "Cylinder 1 Misfire Detected"
          },
          "threeByte": {
            "number": "P0301",
            "ftb": "0",
            "description": "Cylinder 1 Misfire Detected",
            "fault": "No Fault Information Available",
            "location": {
              "sensor": "",
              "bank": "",
              "circuit": "",
              "valve": "",
              "cylinder": 1,
              "camshaft": "",
              "solenoid": "",
              "regulator": "",
              "controlModule": "",
              "audioAmplifier": "",
              "processingModule": ""
            }
          },
          "links": {
            "self": "https://diagnostic.vin.li/api/v1/codes/313cc7d7-1ad6-491k-9e02-a3f48e62984a"
          }
        }
      }


Battery Status
``````````````
This provides a general health status for a vehicle's battery. Possible statuses include:
 * `green` indicates that the battery is likely to start
 * `yellow` indicates that the battery may have issues starting
 * `red` indicates a battery is likely to not start
 * `null` indicates that Vinli could not determine the status based on the data provided


 Request
 +++++++
 .. code-block:: json

       GET https://diagnostic.vin.li/api/v1/vehicles/38ff2972-7fd2-4319-8389-b9a8b84a7c8f/battery_statuses/_current


       Response
       ++++++++
       .. code-block:: json

             HTTP/1.1 200 OK
             Content-Type: application/json

             {
                "batteryStatus": {
                  "status": "green",
                  "timestamp": "2016-08-21T20:00:22.680Z"
                }
              }
