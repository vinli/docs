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

* `distance` - total distance traveled (in meters) by the vehicle during this Trip
* `duration` - time (in milliseconds) between the start and end of this trip
* `averageSpeed` - average speed (in kph) of the trip
* `averageMovingSpeed` - average speed while the vehicle was in motion (eliminates times when the vehicle had a speed of 0)
* `stdDevMovingSpeed` - the standard deviation of the speed while the vehicle was in motion
* `maxSpeed` - the maximum speed (in kph) reported for the Vehicle during the Trip
* `stopCount` - the number of times the Vehicle came to a stop (excludes the beginning and end of the Trip)

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
          "startLocation" : {
            "type": "Feature",
            "geometry": {
              "type": "Point",
              "coordinates": [-100.0, 31.0]
            },
            "properties": {
              "name": "Start Location"
            }
          },
          "stopLocation" : {
            "type": "Feature",
            "geometry": {
              "type": "Point",
              "coordinates": [-96.0, 32.0]
            },
            "properties": {
              "name": "Stop Location"
            }
          },
          "status" : "complete",
          "deviceId" : "821374c0-d6d8-11e3-9c1a-0800200c9a66",
          "vehicleId" : "27b8db50-1274-11e4-9191-0800200c9a66",
          "distance" : 2304,
          "duration" : 147413,
          "averageSpeed" : 56.3,
          "averageMovingSpeed" : 67.52,
          "stdDevMovingSpeed" : 10.39,
          "maxSpeed" : 112.4,
          "stopCount" : 14,
          "links" : {
            "self" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45",
            "snapshots" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots",
            "messages" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/messages",
            "locations" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/locations"
          }
        }
      }
