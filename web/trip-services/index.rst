Trip Service
============

The Vinli device detects vehicle ignition and shutdown and sends those events to the platform.  From these events, it is possible to organize the telemetry data into logical "Trips" for organizing users' activities in your application.  The Trip Service provides access to a catalog of these Trips by Device or by Vehicle and provides mirrors of the Telemetry Services methods centered around these Trips.

It's important to note that trips are sometimes created asyncrhonously--either because they have to be constructed by post-processing or after bulk data upload for a given device.


List All of a Device's Trips
````````````````````````````

This method returns a list of all trips that a given device has taken.  This will include trips that have not yet been completed.


Request
+++++++

.. code-block:: json

      GET https://trips.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/trips
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "trips": [
          {
            "id" : "e960a385-0ced-4654-8404-3238e147ad45",
            "start" : "2014-07-23T14:17:18.324Z",
            "stop" : "2014-07-23T14:19:45.737Z",
            "status" : "complete",
            "vehicleId" : "27b8db50-1274-11e4-9191-0800200c9a66",
            "links" : {
              "self" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45",
              "snapshots" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots",
              "locations" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/locations",
              "vehicle" : "https://platform.vin.li/api/v1/vehicles/27b8db50-1274-11e4-9191-0800200c9a66"
            }
          },
          ...
        ],
        "meta": {
          "pagination" : {
            "totalCount" : 14,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "https://trips.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/trips?offset=0&limit=10",
              "next" : "https://trips.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/trips?offset=10&limit=10",
              "last" : "https://trips.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/trips?offset=10&limit=10"
            }
          }
        }
      }


List All of a Vehicle's Trips
`````````````````````````````

This method returns a list of all trips that a given vehicle has taken.  This will include trips that have not yet been completed.  This list will include only trips for the vehicle for which the current application has access to the associated device.

Please note, that trips are sometimes created asynchronously--either because they have to be constructed by post-processing or after bulk data upload for a given device.


Request
+++++++

.. code-block:: json

      GET https://trips.vin.li/api/v1/vehicle/27b8db50-1274-11e4-9191-0800200c9a66/trips
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "trips": [
          {
            "id" : "e960a385-0ced-4654-8404-3238e147ad45",
            "start" : "2014-07-23T14:17:18.324Z",
            "stop" : "2014-07-23T14:19:45.737Z",
            "status" : "complete",
            "vehicleId" : "27b8db50-1274-11e4-9191-0800200c9a66",
            "links" : {
              "self" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45",
              "snapshots" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots",
              "locations" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/locations"
            }
          },
          ...
        ],
        "meta": {
          "pagination" : {
            "totalCount" : 14,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "https://trips.vin.li/api/v1/vehicle/27b8db50-1274-11e4-9191-0800200c9a66/trips?offset=0&limit=10",
              "next" : "https://trips.vin.li/api/v1/vehicle/27b8db50-1274-11e4-9191-0800200c9a66/trips?offset=10&limit=10",
              "last" : "https://trips.vin.li/api/v1/vehicle/27b8db50-1274-11e4-9191-0800200c9a66/trips?offset=10&limit=10"
            }
          }
        }
      }



Get Details of a Trip
`````````````````````

For each trip, more detailed information regarding overall trip statistics is available here. This includes start and stop location as well as a few other statistical information which may be of interest.  These items include:

* `averageLoad` - average engine load (in percent) of the trip
* `averageMovingSpeed` - average speed while the vehicle was in motion (eliminates times when the vehicle had a speed of 0)
* `averageSpeed` - average speed (in kph) of the trip
* `distance` - total distance traveled (in meters) by the vehicle during this Trip
* `distanceByGPS` - total distance traveled (in meters) according to GPS.  This is more accurate for longer trips, but for shorter trips, it may be inaccurate due to the time to get a fix at the start of a trip.
* `distanceByVSS` - total distance traveled (in meters) according to the speed of the vehicle.  This tends to be more accurate over shorter time periods.
* `duration` - time (in milliseconds) between the start and end of this trip
* `fuelConsumed` - estimated amount of fuel (in liters) consumed during this trip
* `fuelEconomy` - estimated fuel economy (in miles per gallon) during this trip
* `hardAccelCount` - the number of times the Vehicle experienced a hard acceleration during this trip
* `hardStopCount` - the number of times the Vehicle experienced a hard stop during this trip
* `maxSpeed` - the maximum speed (in kph) reported for the Vehicle during the Trip
* `stdDevMovingSpeed` - the standard deviation of the speed while the vehicle was in motion
* `stopCount` - the number of times the Vehicle came to a stop

Request
+++++++

.. code-block:: json

      GET https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "trip": {
          "id" : "e960a385-0ced-4654-8404-3238e147ad45",
          "start" : "2014-07-23T14:17:18.324Z",
          "stop" : "2014-07-23T14:19:45.737Z",
          "startLocation" :  {
            "type": "Point",
            "coordinates": [-100.0, 31.0]
          },
          "stopLocation" : {
            "type": "Point",
            "coordinates": [-96.0, 32.0]
          },
          "status" : "complete",
          "deviceId" : "821374c0-d6d8-11e3-9c1a-0800200c9a66",
          "vehicleId" : "27b8db50-1274-11e4-9191-0800200c9a66",
          "stats" : {
            "averageLoad" : 67.92,
            "averageMovingSpeed" : 67.52,
            "averageSpeed" : 56.3,
            "distance" : 2304,
            "distanceByVSS" : 2289,
            "distanceByGPS" : 2304,
            "duration" : 147413,
            "fuelConsumed" : 3.294,
            "fuelEconomy" : 25.90,
            "hardAccelCount" : 2,
            "hardBrakeCount" : 0,
            "maxSpeed" : 112.4,
            "stdDevMovingSpeed" : 10.39,
            "stopCount" : 14
          }
          "links" : {
            "self" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45",
            "snapshots" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots",
            "messages" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/messages",
            "locations" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/locations"
          }
        }
      }
