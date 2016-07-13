Distance API
------------
A vehicles Odometer reading is not exposed through the OBDII port. However, knowing this reading can be handy in many use cases... thus we created Distance Service. Distance Service is our best effort guess at what the actual odometer of a car is at present time and/or to provide the milage travelled between 2 points in time.

**All distances are in meters.**

Get All of a Vehicles Distances
```````````````````````````````
This method returns a list of all distances (or odometer readings) that have been created for a vehicle.

Request
+++++++
.. code-block:: json

      GET https://distance.vin.li/api/v1/vehicles/{vehicleId}/distances
      Accept: application/json

Optionally - this method accepts ``since`` and ``until`` query parameters.
You may also pass ``x-vinli-unit`` in the header with either ``km``, ``mi``, or ``m`` to modify the output units. Defaults to ``m``.

Response
++++++++
.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json
 {
  "distances": [
    {
      "confidenceMin": 38270282.779,
      "confidenceMax": 128122251.041,
      "value": 83196266.91,
      "lastOdometerDate": "2016-02-24T20:59:53.633Z"
    }
  ]
 }

Details for Distances
*********************
 * *confidenceMin* - the minimum range value for the predicted odometer reading
 * *confidenceMax* - the maximum range value for the predicted odometer reading
 * *value* - the best guess odometer value
 * *lastOdometerDate* - the date/time of the most recent odometer record


Create an Odometer Report
``````````````````````````
Request
+++++++
.. code-block:: json

 POST https://distance.vin.li/api/v1/vehicles/{vehicleId}/odometers
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

      GET https://distance.vin.li/api/v1/vehicles/{vehicleId}/odometers
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
      "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/0e14f2db-ff0b-43bd-b88c-01b9f226778f"
      }
    }
  }


Delete an Odometer Report
`````````````````````````
Request
+++++++
.. code-block:: json

 DELETE https://distance.vin.li/api/v1/odometers/{odometerId}


Odometer Triggers
`````````````````
Odometer triggers generate events/notifications for milage thresholds that you define.

 * `type` - Required. There are 3 types of triggers, `specific`, `from_now`, `milestone`

  * `specific`: when an odometer hits a certain distance i.e. 50k miles
  * `from_now`: when an odometer hits a certain distance greater than the current distance
  * `milestone`: when an odometer hits a certain recurring interval i.e. every 5k miles

 * `threshold` - Required. The amount for your `type`.
 * `unit` - Required. The unit of measure of the `threshold`. Accepts `km`, `mi`, or `m`.

Once an Odometer Trigger is set, `Events <http://docs.vin.li/en/latest/web/event-services/index.html>`_  will be created when the trigger criteria are met.

Create an Odometer Trigger
``````````````````````````
Request
+++++++
.. code-block:: json

 POST https://distance.vin.li/api/v1/vehicles/{vehicleId}/odometer_triggers
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
        "vehicle": "https://platform.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31"
      }
    }
    }



Get an Odometer Trigger
```````````````````````
Request
+++++++
.. code-block:: json

 GET https://distance.vin.li/api/v1/odometer_triggers/{odometerTriggerId}

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
    "vehicle": "https://platform.vin.li/api/v1/vehicles/ab4e7199-a3a6-412f-9088-bc05b6d89e31"
  }
 }


Delete an Odometer Trigger
``````````````````````````
Request
+++++++
.. code-block:: json

 DELETE https://distance.vin.li/api/v1/odometer_triggers/{odometerTriggerId}



Get All Odometer Triggers for a Vehicle
```````````````````````````````````````
Request
+++++++
.. code-block:: json

 GET https://distance.vin.li/api/v1/vehicles/{vehicleId}/odometer_triggers

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
