Distance API
------------
A vehicles Odometer reading is not exposed through the OBDII port. However, knowing this reading can be handy in many use cases... thus we created Distance Service. Distance Service is our best effort guess at what the actual odometer of a car is at present time and/or to provide the distance travelled between 2 points in time.

**All distances are in meters.**

Get Latest Distance for a Vehicle
`````````````````````````````````
This method returns the most current distance estimate for a given vehicle.

Request
+++++++
.. code-block:: json

      GET https://distance.vin.li/api/v1/vehicles/36cf2965-7ed1-4314-8384-f9b6b75a7d3f/distances/_latest
      Accept: application/json

Optionally - this method accepts ``since`` and ``until`` query parameters.
You may also pass ``x-vinli-unit`` in the header with either ``km``, ``mi``, or ``m`` to modify the output units. Defaults to ``m``.

Response
++++++++
.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "distance": {
          "vehicleId": "36cf2965-7ed1-4314-8384-f9b6b75a7d3f",
          "value": 94338300.26,
          "unit": "m",
          "confidenceMin": 94337300.26,
          "confidenceMax": 94339300.26,
          "lastOdometerDate": "2016-12-09T23:00:36.755Z",
          "links": {
            "self": "https://distance.vin.li/api/v1/vehicles/36cf2965-7ed1-4314-8384-f9b6b75a7d3f/distances/_latest?since=1970-01-01T00:00:00.000Z&until=2016-12-20T22:29:57.292Z",
            "vehicle": "https://platform.vin.li/api/v1/vehicles/36cf2965-7ed1-4314-8384-f9b6b75a7d3f"
          }
        }
      }


Create an Odometer Reading
```````````````````````````
Request
+++++++
.. code-block:: json

 POST https://distance.vin.li/api/v1/vehicles/{vehicleId}/odometers
 Accept: application/json
 Content-Type: application/json

   {
    "odometer": {
     "reading": 15000,
     "date": "2016-04-26T17:01:36.243Z",
     "unit": "km"
    }
   }

* `reading` - Required. The odometer value you are submitting.
* `date` - The date/time at which this odometer reading applies. Optional, defaults to now.
* `unit` - Required. the unit of measure of the `reading`. Accepts `km`, `mi`, or `m`.

Response
++++++++
.. code-block:: json

 HTTP/1.1 200 OK
 Content-Type: application/json

  {
    "odometer": {
      "id": "c6e3fbb7-c1e8-4de3-8c38-75661dd9cd40",
      "vehicleId": "484ceb75-87ba-4813-b414-1c13f2056325",
      "reading": 15000000,
      "unit": "m",
      "date": "2016-12-20T22:35:39.504Z",
      "links": {
        "self": "https://distance.vin.li/api/v1/odometers/c6e3fbb7-c1e8-4de3-8c38-75661dd9cd40",
        "vehicle": "https://platform.vin.li/api/v1/vehicles/484ceb75-87ba-4813-b414-1c13f2056325"
      }
    }
  }

Get All Odometer Readings for a Vehicle
```````````````````````````````````````
Request
+++++++
.. code-block:: json

      GET https://distance.vin.li/api/v1/vehicles/ec74e512-ed9a-41ae-99e9-779882846b80/odometers
      Accept: application/json

Response
++++++++
.. code-block:: json

 HTTP/1.1 200 OK
 Content-Type: application/json

 {
  "odometers": [
   {
     "id": "5b32bcad-a127-40fd-a0f9-c14bc283e255",
     "vehicleId": "ec74e512-ed9a-41ae-99e9-779882846b80",
     "reading": 1720.17,
     "date": "2016-02-09T16:56:31.033Z",
     "links": {
       "self": "https://distance.vin.li/api/v1/odometers/be7baede-c865-3e9c-8181-8126c332683d",
       "vehicle": "https://platform.vin.li/api/v1/vehicles/ec74e512-ed9a-41ae-99e9-779882846b80"
     }
   },
   {
     "id": "59dd31f2-8101-4f1f-9539-6580668e719e",
     "vehicleId": "ec74e512-ed9a-41ae-99e9-779882846b80",
     "reading": 4640.85,
     "date": "2016-02-02T16:56:31.033Z",
     "links": {
       "self": "https://distance.vin.li/api/v1/odometers/be7baede-c865-3e9c-8181-8126c332683d",
       "vehicle": "https://platform.vin.li/api/v1/vehicles/ec74e512-ed9a-41ae-99e9-779882846b80"
     }
   }
 ],
 "meta": {
   "pagination": {
     "remaining": 0,
     "until": "2016-02-16T16:56:31.036Z",
     "since": "1970-01-01T00:00:00.000Z",
     "limit": 20,
     "sortDir": "desc",
     "links": {}
   }
 }
 }


Get an Odometer
```````````````
Request
+++++++
.. code-block:: json

 GET https://distance.vin.li/api/v1/odometers/{odometerId}
 Accept: application/json

Response
++++++++
.. code-block:: json

   HTTP/1.1 200 OK
   Content-Type: application/json

 {
  "odometer": {
    "id": "bcdc8734-ce79-4d78-a911-f77c09316f5f",
    "vehicleId": "0e14f2db-ff0b-43bd-b88c-01b9f226778f",
    "reading": 83321969.16,
    "date": "2016-03-03T20:23:53.726Z",
    "links": {
      "self": "https://distance.vin.li/api/v1/odometers/bcdc8734-ce79-4d78-a911-f77c09316f5f",
      "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/0e14f2db-ff0b-43bd-b88c-01b9f226778f"
      }
    }
  }


Delete an Odometer Reading
``````````````````````````
Request
+++++++
.. code-block:: json

 DELETE https://distance.vin.li/api/v1/odometers/bcdc8734-ce79-4d78-a911-f77c09316f5f


Odometer Triggers
`````````````````
Odometer triggers generate events/notifications for milage thresholds that you define.

 * `type` - Required. There are 3 types of triggers, `specific`, `from_now`, `milestone`

  * `specific`: when an odometer hits a certain distance i.e. 50k miles
  * `from_now`: when an odometer hits a specific distance traveled from now
  * `milestone`: when an odometer hits a certain recurring interval i.e. every 5k miles

 * `threshold` - Required. The amount for your `type`.
 * `unit` - Required. The unit of measure of the `threshold`. Accepts `km`, `mi`, or `m`.

Once an Odometer Trigger is set, `Events <http://docs.vin.li/en/latest/web/event-services/index.html>`_  will be created when the trigger criteria are met.

Create an Odometer Trigger
``````````````````````````
Request
+++++++
.. code-block:: json

 POST https://distance.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31/odometer_triggers
 Accept: application/json
 Content-Type: application/json

 {
 "odometerTrigger": {
  "type": "specific",
  "threshold": 5000000,
  "unit": "km"
  }
 }

Response
++++++++
.. code-block:: json

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "odometerTrigger": {
        "id": "2b45bf31-b920-4afd-be1f-32b3f867bc4a",
        "vehicleId": "ab4e7199-a3a6-412f-9088-bc05b6d89e31",
        "type": "from_now",
        "threshold": 9496.086,
        "events": 0,
        "links": {
          "self": "https://distance.vin.li/api/v1/odometer_triggers/2b45bf31-b920-4afd-be1f-32b3f867bc4a",
          "vehicle": "https://platform.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31"
        }
      }
    }



Get an Odometer Trigger
```````````````````````
Request
+++++++
.. code-block:: json

 GET https://distance.vin.li/api/v1/odometer_triggers/2b45bf31-b920-4afd-be1f-32b3f867bc4a

Response
++++++++

.. code-block:: json

 "odometerTrigger": {
  "id": "2b45bf31-b920-4afd-be1f-32b3f867bc4a",
  "vehicleId": "ab4e7199-a3a6-412f-9088-bc05b6d89e31",
  "type": "from_now",
  "threshold": 9496.086,
  "events": 0,
  "links": {
    "self": "https://distance.vin.li/api/v1/odometer_triggers/2b45bf31-b920-4afd-be1f-32b3f867bc4a",
    "vehicle": "https://platform.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31"
  }
 }


Delete an Odometer Trigger
``````````````````````````
Request
+++++++
.. code-block:: json

 DELETE https://distance.vin.li/api/v1/odometer_triggers/2b45bf31-b920-4afd-be1f-32b3f867bc4a



Get All Odometer Triggers for a Vehicle
```````````````````````````````````````
Request
+++++++
.. code-block:: json

 GET https://distance.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31/odometer_triggers

Response
++++++++
.. code-block:: json

 HTTP/1.1 200 OK
 Content-Type: application/json

     {
        "odometerTriggers": [
          {
            "id": "2b45bf31-b920-4afd-be1f-32b3f867bc4a",
            "vehicleId": "ab4e7199-a3a6-412f-9088-bc05b6d89e31",
            "type": "specific",
            "threshold": 5000000000,
            "unit": "m",
            "events": 0,
            "links": {
              "self": "https://distance.vin.li/api/v1/odometer_triggers/2b45bf31-b920-4afd-be1f-32b3f867bc4a",
              "vehicle": "https://platform.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31"
            }
          },
          {
            "id": "6c35bf31-c120-5afd-ae1c-22b3c867fc4f",
            "vehicleId": "ab4e7199-a3a6-412f-9088-bc05b6d89e31",
            "type": "specific",
            "threshold": 5000000000,
            "unit": "m",
            "events": 0,
            "links": {
              "self": "https://distance.vin.li/api/v1/odometer_triggers/6c35bf31-c120-5afd-ae1c-22b3c867fc4f",
              "vehicle": "https://platform.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31"
            }
          }
        ],
        "meta": {
          "pagination": {
            "remaining": 0,
            "until": "2016-12-20T22:48:48.058Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 20,
            "sortDir": "desc",
            "links": {}
          }
        }
      }
