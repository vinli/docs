Distance API
------------
A vehicles Odometer reading is exposed through the OBDII port. However, knowing this reading can be handy in many use cases... thus we created Distance Service. Distance Service is our best effort guess at what the actual odometer of a car is at present time and/or to provide the milage travelled between 2 points in time.

**All distances are in meters.**

Get All of a Vehicles Distances
```````````````````````````````
This method returns a list of all distances (or odemeter readings) that have been created for a vehicle.

Request
+++++++
.. code-block:: json

      GET https://distances.vin.li/api/v1/vehicles/{vehicleId}/distances/
      Accept: application/json

Optionally - this method accepts ``from`` and ``until`` query parameters.

Response
++++++++
.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
      "distances": [
        {
          "confidenceMin": 6300.627,
          "confidenceMax": 38703.855,
          "value": 22502.241,
          "confidence": 0.28,
          "source": "trips",
          "lastOdometerDate": "2016-02-02T16:29:53.616Z"
        },
        {
          "confidenceMin": 2894918,
          "confidenceMax": 2896918,
          "value": 2895918,
          "confidence": 1,
          "source": "dtc",
          "lastOdometerDate": "2016-02-02T16:29:53.616Z"
        }
      ],
      "links": {
        "vehicle": "https://platform.vin.li/api/v1/vehicles/5d41c2b4-5fae-48e3-ac0a-f8df675f6c75"
      }
      }

Details for Distances
*********************
 * *confidenceMin* - the minimum range odometer value based on the confidence rating
 * *confidenceMax* - the maximum range odometer value based on the confidence rating
 * *value* - the best guess odometer value
 * *confidence* - 0-1 rating that indicates the likelihood of accuracy for the distance reading (0 being least accurate and 1 being most accurate)
 * *source* - the source by which the distance was derived
 * *lastOdometerDate* - the date/time of the most recent odometer record

Sources
*******
Odometers can be obtained via 1 of 2 sources.
 * *dtc* - vehicles compile the milage driven since the dtc codes were last cleared. This is a highly accurate milage reading.
 * *trips* - odometers sourced from trips summarize trip distances recorded by Vinli. This is a less accurate measure.

Create an Odometer Report
``````````````````````````
Request
+++++++
.. code-block:: json

 POST https://distances.vin.li/api/v1/vehicles/{vehicleId}/odometers/
 Accept: application/json
 Content-Type: application/json

   {
    "odometer": {
     "reading": 15000,
     "date": "2016-02-16T17:01:36.243Z",
     "unit": "km"
    }
   }

* `reading` - Required. The odometer value you are submitting.
* `date` - The date/time at which this odometer reading applies. Optional, defaults to now.
* `unit` - the unit of measure of the `reading`. Accepts `km`, `mi`, or `m`.

Response
++++++++
.. code-block:: json

 HTTP/1.1 200 OK
 Content-Type: application/json
  {
    "odometer": {
      "id": "c6e3fbb7-c1e8-4de3-8c38-75661dd9cd40",
      "vehicleId": "484ceb75-87ba-4813-b414-1c13f2056325",
      "reading": 640.325,
      "date": "2016-02-16T16:55:20.707Z",
      "links": {
        "vehicle": "https://platform.vin.li/api/v1/vehicles/484ceb75-87ba-4813-b414-1c13f2056325"
      }
    }
  }

List All Odometer Reports for a Vehicle
```````````````````````````````````````
Request
+++++++
.. code-block:: json

      GET https://distances.vin.li/api/v1/vehicles/{vehicleId}/odometers/
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
       "vehicle": "https://platform.vin.li/api/v1/vehicles/ec74e512-ed9a-41ae-99e9-779882846b80"
     }
   },
   {
     "id": "59dd31f2-8101-4f1f-9539-6580668e719e",
     "vehicleId": "ec74e512-ed9a-41ae-99e9-779882846b80",
     "reading": 4640.85,
     "date": "2016-02-02T16:56:31.033Z",
     "links": {
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

Create an Odometer Trigger
``````````````````````````
Request
+++++++
.. code-block:: json

 POST https://distances.vin.li/api/v1/vehicles/{vehicleId}/odometers_triggers
 Accept: application/json
 Content-Type: application/json

 {
 "odometerTrigger": {
  "type": "specific",
  "threshold": 5000000
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
        "vehicle": "https://platform.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31"
      }
    }
    }


Details for Odometer Triggers
*****************************
* `type` - there are 3 types of triggers, `specifc`, `from_now`, `milestone`

 * `specific`: when an odometer hits a certain distance i.e. 50k miles
 * `from_now`: when an odometer hits a certain distance greater than the current distance
 * `milestone`: when an odometer hits a certain recurring interval i.e. every 5k miles


Delete an Odometer Trigger
``````````````````````````
Request
+++++++
.. code-block:: json

 DELETE https://distances.vin.li/api/v1/odometer_triggers/{odometerTriggerId}



Get All Odometer Triggers for a Vehicle
```````````````````````````````````````
Request
+++++++
.. code-block:: json

 GET https://distances.vin.li/api/v1/vehicles/{vehicleId}/odometers_triggers

Response
++++++++
.. code-block:: json

 HTTP/1.1 200 OK
 Content-Type: application/json

     {
     "odometerTriggers": [
       {
         "id": "a65c249f-083d-4d44-951c-a44467422192",
         "vehicleId": "a657fbac-1e29-474f-846c-49bd63f92e12",
         "type": "specific",
         "threshold": 777.38,
         "events": 0,
         "links": {
           "vehicle": "https://platform.vin.li/api/v1/vehicles/a657fbac-1e29-474f-846c-49bd63f92e12"
         }
       }
     ]
     }
