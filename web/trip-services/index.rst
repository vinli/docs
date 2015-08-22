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

      GET https://trips.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/trips
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "id": "a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
        "start": "2015-08-19T19:25:15.951Z",
        "stop": "2015-08-19T19:35:28.875Z",
        "status": "completed",
        "vehicleId": "0c785aa0-1a48-4cc6-9f5c-028350dd907d",
        "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
        "startPoint": {
          "type": "point",
          "coordinates": [
            -96.789791,
            32.780046
          ]
        },
        "stopPoint": {
          "type": "point",
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
          "stopCount": 8
        },
        "links": {
          "self": "https://trips-dev.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
          "device": "https://platform-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d",
          "locations": "https://telemetry-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/locations?since=1440012315951&until=1440012928875",
          "messages": "https://telemetry-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/messages?since=1440012315951&until=1440012928875",
          "events": "https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/events?since=1440012315951&until=1440012928875"
        }
      }


List All of a Vehicle's Trips
`````````````````````````````

This method returns a list of all trips that a given vehicle has taken.  This will include trips that have not yet been completed.  This list will include only trips for the vehicle for which the current application has access to the associated device.

Please note, that trips are sometimes created asynchronously--either because they have to be constructed by post-processing or after bulk data upload for a given device.


Request
+++++++

.. code-block:: json

      GET https://trips.vin.li/api/v1/vehicles/27b8db50-1274-11e4-9191-0800200c9a66/trips
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "id": "a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
        "start": "2015-08-19T19:25:15.951Z",
        "stop": "2015-08-19T19:35:28.875Z",
        "status": "completed",
        "vehicleId": "0c785aa0-1a48-4cc6-9f5c-028350dd907d",
        "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
        "startPoint": {
          "type": "point",
          "coordinates": [
            -96.789791,
            32.780046
          ]
        },
        "stopPoint": {
          "type": "point",
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
          "stopCount": 8
        },
        "links": {
          "self": "https://trips-dev.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
          "device": "https://platform-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d",
          "locations": "https://telemetry-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/locations?since=1440012315951&until=1440012928875",
          "messages": "https://telemetry-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/messages?since=1440012315951&until=1440012928875",
          "events": "https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/events?since=1440012315951&until=1440012928875"
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
* `hardBrakeCount` - the number of times the Vehicle experienced a hard stop during this trip
* `maxSpeed` - the maximum speed (in kph) reported for the Vehicle during the Trip
* `stdDevMovingSpeed` - the standard deviation of the speed while the vehicle was in motion
* `stopCount` - the number of times the Vehicle came to a stop

All of the detailed information listed in the above verbiage is available via the get trips by device or get trips by vehicle.

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
        "id": "a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
        "start": "2015-08-19T19:25:15.951Z",
        "stop": "2015-08-19T19:35:28.875Z",
        "status": "completed",
        "vehicleId": "0c785aa0-1a48-4cc6-9f5c-028350dd907d",
        "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
        "startPoint": {
          "type": "point",
          "coordinates": [
            -96.789791,
            32.780046
          ]
        },
        "stopPoint": {
          "type": "point",
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
          "stopCount": 8
        },
        "links": {
          "self": "https://trips-dev.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
          "device": "https://platform-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d",
          "locations": "https://telemetry-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/locations?since=1440012315951&until=1440012928875",
          "messages": "https://telemetry-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/messages?since=1440012315951&until=1440012928875",
          "events": "https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/events?since=1440012315951&until=1440012928875"
        }
      }
