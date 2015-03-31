Trip Service
------------

### List All of a Device's Trips

This method returns a list of all trips that a given device has taken.  This will include trips that have not yet been completed.


#### Request

      GET https://trips.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/trips
      Accept: application/json


#### Response

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


### List All of a Vehicle's Trips

This method returns a list of all trips that a given vehicle has taken.  This will include trips that have not yet been completed.  This list will include only trips for the vehicle for which the current application has access to the associated device.

Please note, that trips are sometimes created asynchronously--either because they have to be constructed by post-processing or after bulk data upload for a given device.


#### Request

      GET https://trips.vin.li/api/v1/vehicle/27b8db50-1274-11e4-9191-0800200c9a66/trips
      Accept: application/json


#### Response

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



### Get Details of a Trip

For each trip, more detailed information regarding overall trip statistics is available here. This includes start and stop location as well as a few other statistical information which may be of interest.  These items include:

* `distance` - total distance traveled (in meters) by the vehicle during this Trip
* `duration` - time (in milliseconds) between the start and end of this trip
* `averageSpeed` - average speed (in kph) of the trip
* `averageMovingSpeed` - average speed while the vehicle was in motion (eliminates times when the vehicle had a speed of 0)
* `stdDevMovingSpeed` - the standard deviation of the speed while the vehicle was in motion
* `maxSpeed` - the maximum speed (in kph) reported for the Vehicle during the Trip
* `stopCount` - the number of times the Vehicle came to a stop (excludes the beginning and end of the Trip)

#### Request

      GET https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45
      Accept: application/json


#### Response

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


Trip Telemetry Proxies
----------------------

The following three methods are essentially proxies of Telemetry Services that enforces a time bound based on the Trip that is referenced.  These are intended to make it easy to paginate through the telemetry data associated with a specific trip without having to construct the URL yourself.

They use the same parameters and return the same results as the original methods, but will stop pagination at either end of the trip.

For more specific information, please refer to the respective sections in "Telemetry Services" above.


### Get Telemetry Snapshots of Trip

See "Telemetry Service - Telemetry Snapshot Service" above.

#### Request

      GET https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType
      Accept: application/json

#### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "snapshots" : [
          {
            "timestamp": "2014-03-13T17:54:20.050Z",
            "vehicleSpeed": 12,
            "calculatedLoadValue": 34.5,
            "fuelType": "Gasoline"
          },
          {
            "timestamp": "2014-03-13T17:54:15.537Z":,
            "vehicleSpeed": 15
          },
          {
            "timestamp": "2014-03-13T17:54:09.898Z",
            "rpm": 3827,
            "calculatedLoadValue": 56.3
          },
          ...
        ],
        "meta" : {
          pagination : {
            "remainingCount" : 1324,
            "limit" : 50,
            "until" : 1394733261450,
            "links" : {
              "latest" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType"
              "prior" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType&until=1394733251897"
            }
          }
        }
      }


### Get Locations of Trip

See "Telemetry Service - Location History Service" above.

#### Request

      GET https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/locations
      Accept: application/json

#### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "locations" : {
          "type" : "FeatureCollection",
          "features" : [
            {
              "type" : "Feature",
              "geometry" : {
                "type" : "Point",
                "coordinates" : [-90.0811, 29.9508]
              },
              "properties" : {
                "timestamp" : "2014-03-13T17:54:20.050Z",
                "rpm" : 1264,
                "vehicleSpeed" : 54
              }
            },
            {
              "type" : "Feature",
              "geometry" : {
                "type" : "Point",
                "coordinates" : [-90.08198, 29.9498]
              },
              "properties" : {
                "timestamp" : "2014-03-13T17:54:07.122Z",
                "rpm" : 1832
              }
            },
            ...
          ]
        },
        "meta" : {
          pagination : {
            "remainingCount" : 1324,
            "limit" : 50,
            "until" : 1394733261450,
            "links" : {
              "latest" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/locations"
              "prior" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/locations&until=1394733251897"
            }
          }
        }
      }


### Get Telemetry Messages of Trip

See "Telemetry Service - Telemetry Message Service" above.

#### Request

      GET https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/messages
      Accept: application/json

#### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "messages" : [
          {
            "timestamp": "2014-07-14T17:46:06.759Z",
            "vehicleSpeed": 12,
            "calculatedLoadValue": 34.5,
            "fuelType": "Gasoline",
            "rpm": 1254,
            "location": {
              "longitude": -90.0811,
              "latitude": 29.9508
            }
          },
          {
            "timestamp": "2014-07-14T17:46:01.544Z",
            "vehicleSpeed": 15,
            "rpm": 1766,
            "location": {
              "longitude": -90.0813,
              "latitude": 29.950802
            }
          },
          {
            "timestamp": "2014-07-14T17:45:54.872Z",
            "vehicleSpeed": 16,
            "calculatedLoadValue": 56.3,
            "rpm": 1766,
            "location": {
              "longitude": -90.08104,
              "latitude": 29.950813
            }
          }
          ...
        ],
        "meta" : {
          pagination : {
            "remainingCount" : 1324,
            "limit" : 50,
            "until" : 1394733261450,
            "links" : {
              "latest" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType"
              "prior" : "https://trips.vin.li/api/v1/trips/e960a385-0ced-4654-8404-3238e147ad45/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType&until=1394733251897"
            }
          }
        }
      }