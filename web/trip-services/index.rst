Trip Service
============

The Vinli device detects vehicle ignition and shutdown and sends those events to the platform.  From these events, it is possible to organize the telemetry data into logical "Trips" for organizing users' activities in your application.  The Trip Service provides access to a catalog of these trips by device or by vehicle and provides mirrors of the Telemetry Services methods centered around these trips.

It's important to note that trips are sometimes created asynchronously--either because they have to be constructed by post-processing or after bulk data upload for a given device.


List All of a Device's Trips
````````````````````````````

This method returns a list of all trips that a given device has taken.  This will include trips that have not yet been completed.


Request
+++++++

.. code-block:: json

      GET https://trips.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/trips
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      "trips: [
        {
          "id": "a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
          "start": "2015-08-19T19:25:15.951Z",
          "stop": "2015-08-19T19:35:28.875Z",
          "status": "completed",
          "vehicleId": "0c785aa0-1a48-4cc6-9f5c-028350dd907d",
          "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "startPoint": {
            "type": "Point",
            "coordinates": [
              -96.789791,
              32.780046
            ]
          },
          "stopPoint": {
            "type": "Point",
            "coordinates": [
              -96.791057,
              32.780671
            ]
          },
          "preview": "ijagEdgwmQtC}B`@Q^w@\\U?ICCBA@BFGBKFIB@OLBCm@cBa@u@W[Uo@c@i@Oq@]_@MCw@z@W?F\\?Fd@c@t@a@f@Td@h@b@n@`@v@`@`@b@n@@?CCEFJv@^lATjAHpA@hAH|@Tz@RvAJd@E^U\\eBbCi@l@WTKl@De@?L@AKPy@z@i@b@Yl@u@jAAPU?sAJmADM[g@aCAgCGIEDJm@h@Q`@ICDGA]kAK}@Yy@Bs@Ve@V[f@M^PVb@Ah@CNSXSGAKBGFD",
          "stats": {
            "averageLoad": 42.6683,
            "averageMovingSpeed": 23.1505,
            "averageSpeed": 15.4892,
            "comprehensiveLocations": true,
            "distance": 2125.35,
            "distanceByGPS": 2051.44,
            "distanceByVSS": 2125.35,
            "duration": 612924,
            "fuelConsumed": 0.358368,
            "fuelEconomy": 15.277,
            "hardAccelCount": null,
            "hardBrakeCount": null,
            "locationCount": 160,
            "maxSpeed": 47,
            "messageCount": 182,
            "stdDevMovingSpeed": 11.0187,
            "stopCount": 8,
            "substantial": true
          },
          "links": {
            "self": "https://trips.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
            "device": "https://platform.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicle": "https://platform.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d",
            "locations": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/locations?since=1440012315951&until=1440012928875",
            "messages": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/messages?since=1440012315951&until=1440012928875",
            "events": "https://events.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/events?since=1440012315951&until=1440012928875"
          }
        }
      ],
      "meta": {
          "pagination": {
            "remaining": 1,
            "until": "2015-06-19T23:59:59.000Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 20,
            "sortDir": "desc",
            "links": {
              "prior": "https://trips-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/trips?until=1434129972999"
            }
          }
        }



List All of a Vehicle's Trips
`````````````````````````````

This method returns a list of all trips that a given vehicle has taken.  This will include trips that have not yet been completed.  This list will include only trips for the vehicle for which the current application has access to the associated device.

Note 1: Trips are sometimes created asynchronously--either because they have to be constructed by post-processing or after bulk data upload for a given device.
Note 2: Only trips for the 20 most recent devices that have been in the vehicle will be returned.


Request
+++++++

.. code-block:: json

      GET https://trips.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d/trips
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "trips": [
          {
            "id": "a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
            "start": "2015-08-19T19:25:15.951Z",
            "stop": "2015-08-19T19:35:28.875Z",
            "status": "completed",
            "vehicleId": "0c785aa0-1a48-4cc6-9f5c-028350dd907d",
            "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "startPoint": {
              "type": "Point",
              "coordinates": [
                -96.789791,
                32.780046
              ]
            },
            "stopPoint": {
              "type": "Point",
              "coordinates": [
                -96.791057,
                32.780671
              ]
            },
            "preview": "ijagEdgwmQtC}B`@Q^w@\\U?ICCBA@BFGBKFIB@OLBCm@cBa@u@W[Uo@c@i@Oq@]_@MCw@z@W?F\\?Fd@c@t@a@f@Td@h@b@n@`@v@`@`@b@n@@?CCEFJv@^lATjAHpA@hAH|@Tz@RvAJd@E^U\\eBbCi@l@WTKl@De@?L@AKPy@z@i@b@Yl@u@jAAPU?sAJmADM[g@aCAgCGIEDJm@h@Q`@ICDGA]kAK}@Yy@Bs@Ve@V[f@M^PVb@Ah@CNSXSGAKBGFD",
            "stats": {
              "averageLoad": 38.288,
              "averageMovingSpeed": 19.9488,
              "averageSpeed": 16.7443,
              "comprehensiveLocations": true,
              "distance": 2467.1,
              "distanceByGPS": 2467.1,
              "distanceByVSS": 2121.67,
              "duration": 503340,
              "fuelConsumed": 0.34644,
              "fuelEconomy": 14.4982,
              "hardAccelCount": 0,
              "hardBrakeCount": 0,
              "locationCount": 433,
              "maxSpeed": 45,
              "messageCount": 557,
              "stdDevMovingSpeed": 12.2787,
              "stopCount": 14,
              "substantial": true
            },
            "links": {
              "self": "https://trips.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
              "device": "https://platform.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
              "vehicle": "https://platform.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d",
              "locations": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/locations?since=1440012315951&until=1440012928875",
              "messages": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/messages?since=1440012315951&until=1440012928875",
              "events": "https://events.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/events?since=1440012315951&until=1440012928875"
            }
          }
        ]
      },
      "meta": {
          "pagination": {
            "remaining": 1,
            "until": "2015-06-19T23:59:59.000Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 20,
            "sortDir": "desc",
            "links": {
              "prior": "https://trips-dev.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d/trips?until=1434129972999"
            }
          }
        }




Get Details of a Trip
`````````````````````

For each trip, more detailed information regarding overall trip statistics is available here. This includes start and stop location as well as other statistical information which may be of interest.  These items include:

* `averageLoad` - average engine load (in percent) of the trip
* `averageMovingSpeed` - average speed while the vehicle was in motion (eliminates times when the vehicle had a speed of 0)
* `averageSpeed` - average speed (in kph) of the trip
* `comprehensiveLocations` - the trip has substantial GPS coverage
* `distance` - total distance traveled (in meters) by the vehicle during this trip
* `distanceByGPS` - total distance traveled (in meters) according to GPS.  This is more accurate for longer trips, but for shorter trips, it may be inaccurate due to the time to get a fix at the start of a trip.
* `distanceByVSS` - total distance traveled (in meters) according to the speed of the vehicle.  This tends to be more accurate over shorter time periods.
* `duration` - time (in milliseconds) between the start and end of this trip
* `fuelConsumed` - estimated amount of fuel (in liters) consumed during this trip
* `fuelEconomy` - estimated fuel economy (in miles per gallon) during this trip
* `hardAccelCount` - the number of times the Vehicle experienced a hard acceleration during this trip
* `hardBrakeCount` - the number of times the Vehicle experienced a hard stop during this trip
* `locationCount` - the number of messages in the trip containing locations
* `maxSpeed` - the maximum speed (in kph) reported for the Vehicle during the trip
* `messageCount` - the total number of messages comprising the trip
* `stdDevMovingSpeed` - the standard deviation of the speed while the vehicle was in motion
* `stopCount` - the number of times the Vehicle came to a stop
* `substantial` - boolean, indicating whether or not a trip had enough messages and data to be considered substantial

All of the detailed information listed in the above verbiage is available via the get trips by device or get trips by vehicle.

* `fuelEconomy` invokes an operation to get the fuel type of a trip. fuelEconomy uses gasoline as the default fuel type. However, diesel will be set as the fuel type (and corresponding diesel values for calculations) if it is detected in a trip.


The trip document also includes short information about the telemetry associated with it, namely:

* `startPoint` - coordinates of the position where the trip was initiated
* `stopPoint` - coordinates of the position where the trip was concluded
* `preview` - encoded string of the polyline representing the trip (usable in map services such as Google Maps, Mapbox, ...)


Request
+++++++

.. code-block:: json

      GET https://trips.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "trip": {
          "id": "a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
          "start": "2015-08-19T19:25:15.951Z",
          "stop": "2015-08-19T19:35:28.875Z",
          "status": "completed",
          "vehicleId": "0c785aa0-1a48-4cc6-9f5c-028350dd907d",
          "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "startPoint": {
            "type": "Point",
            "coordinates": [
              -96.789791,
              32.780046
            ]
          },
          "stopPoint": {
            "type": "Point",
            "coordinates": [
              -96.791057,
              32.780671
            ]
          },
          "preview": "ijagEdgwmQtC}B`@Q^w@\\U?ICCBA@BFGBKFIB@OLBCm@cBa@u@W[Uo@c@i@Oq@]_@MCw@z@W?F\\?Fd@c@t@a@f@Td@h@b@n@`@v@`@`@b@n@@?CCEFJv@^lATjAHpA@hAH|@Tz@RvAJd@E^U\\eBbCi@l@WTKl@De@?L@AKPy@z@i@b@Yl@u@jAAPU?sAJmADM[g@aCAgCGIEDJm@h@Q`@ICDGA]kAK}@Yy@Bs@Ve@V[f@M^PVb@Ah@CNSXSGAKBGFD",
          "stats": {
            "averageLoad": 38.288,
            "averageMovingSpeed": 19.9488,
            "averageSpeed": 16.7443,
            "comprehensiveLocations": true,
            "distance": 2467.1,
            "distanceByGPS": 2467.1,
            "distanceByVSS": 2121.67,
            "duration": 503340,
            "fuelConsumed": 0.34644,
            "fuelEconomy": 14.4982,
            "hardAccelCount": 0,
            "hardBrakeCount": 0,
            "locationCount": 433,
            "maxSpeed": 45,
            "messageCount": 557,
            "stdDevMovingSpeed": 12.2787,
            "stopCount": 14,
            "substantial": true
          },
          "links": {
            "self": "https://trips.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
            "device": "https://platform.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicle": "https://platform.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d",
            "locations": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/locations?since=1440012315951&until=1440012928875",
            "messages": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/messages?since=1440012315951&until=1440012928875",
            "events": "https://events.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/events?since=1440012315951&until=1440012928875"
          }
        }
      }

.. toctree::
  :maxdepth: 2
