Vinli API Reference
===================

Device API
----------

List all Devices
````````````````

This returns a paginated list of devices that are registered with your application sorted chronologically by when the device was added.

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "devices" : [
          {
            "id" : "8b8a1810-d6d8-11e3-9c1a-0800200c9a66",
            "name" : "testdevice001",
            "links" : {
              "self" : "https://platform.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66",
              "vehicles" : "https://platform.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/vehicles",
              "latestVehicle" : "https://platform.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "total" : 1431,
            "offset" : 0,
            "limit" : 20,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/devices?offset=0&limit=20",
              "last" : "https://platform.vin.li/api/v1/devices?offset=1420&limit=20",
              "next" : "https://platform.vin.li/api/v1/devices?offset=20&limit=20"
            }
          }
        }
      }


Get a Device
````````````

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "device" : {
          "id" : "821374c0-d6d8-11e3-9c1a-0800200c9a66",
          "links" : {
            "self" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66",
            "groups" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups",
            "vehicles" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles",
            "latestVehicle" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest"
          }
        }
      }


Register a Device
`````````````````

.. note:: This route is only accessible by Enterprise applications.  Consumer applications gain and lose devices as users authorize access via the OAuth flow in MyVinli.


Your application may register a device after it has been authorized by the owner of the device (See section above on "Authentication for User Actions").  This step is necessary before your application can access any data from the device or perform any actions on the device.

A two-step process allow you to manage device authorization independent of user action.  You can remove a device without requiring a user to revoke access to the device.


Request
+++++++

.. code-block:: json

      POST https://platform.vin.li/api/v1/devices
      Content-Type: application/json
      Accept: application/json

      {
        "device" : {
          "id" : "821374c0-d6d8-11e3-9c1a-0800200c9a66"
        }
      }

Response
++++++++

.. code-block:: json

      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66

      {
        "device" : {
          "id" : "821374c0-d6d8-11e3-9c1a-0800200c9a66",
          "links" : {
            "self" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66",
            "groups" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups",
            "vehicles" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles",
            "latestVehicle" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest"
          }
        }
      }


Deregister a Device
```````````````````

.. note:: This route is only accessible by Enterprise applications.  Consumer applications gain and lose devices as users authorize access via the OAuth flow in MyVinli.

Deregistering a Device from your application prevents you from accessing that device's data.  Note this has several various effects on other section of the Vinli Platform.  For instance,  Event Services will remove any Rules associated with the device, Safety Services will remove any Emergency Contact actions from the Device (if your application registered the Device with Safety Services), and Diagnostic Services will remove any DTC alerts for this Device registered by your Application.

It's important to note that deregistering a Device is an Application-level action that will have no effect on any other Application (yours or someone else's) that has been authorized for the Device.


Request
+++++++

.. code-block:: json

      DELETE https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66


Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT

Vehicle API
-----------
List All of a Device's Vehicles
```````````````````````````````


Returns the vehicles associated with the given device in chronological order.


Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicles" : [
          {
            "id" : "67e1e940-d6da-11e3-9c1a-0800200c9a66",
            "year" : "2007",
            "make" : "Toyota",
            "model" : "Camry",
            "trim" : "SE V6",
            "vin" : "2B4GP44R6WR942762",
            "links" : {
              "self" : "https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66",
              "trips" : "https://trip.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/trips",
              "collisions" : "https://safety.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/collisions",
              "reportCards" : "https://behavioral.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/reportCards"
            }
          },
          {
            "id" : "2a88b0f0-d6db-11e3-9c1a-0800200c9a66",
            "vin" : "JE3BW50W4NZ676124",
            "links" : {
              "self" : "https://platform.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66",
              "trips" : "https://trip.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66/trips",
              "collisions" : "https://safety.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66/collisions",
              "reportCards" : "https://behavioral.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66/reportCards"
            }
          },
          ...
        ],
        "meta": {
          "pagination" : {
            "total" : 24,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles?offset=0&limit=10",
              "next" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles?offset=10&limit=10",
              "last" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles?offset=20&limit=10"
            }
          }
        }
      }


List a Device's Latest Vehicle
``````````````````````````````


Returns the vehicle most recently associated with the given device if it exists.  If the device has not been associated with a vehicle, a null vehicle object is returned.

Basic vehicle information is returned as part of this response.  Follow the vehicle's "self" link to get full detailed information about the vehicle.

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicle" : {
          "id" : "67e1e940-d6da-11e3-9c1a-0800200c9a66",
          "year" : "2007",
          "make" : "Toyota",
          "model" : "Camry",
          "trim" : "SE V6",
          "vin" : "2B4GP44R6WR942762",
          "links" : {
            "self" : "https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66",
            "trips" : "https://trip.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/trips",
            "collisions" : "https://safety.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/collisions",
            "reportCards" : "https://behavioral.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/reportCards"
          }
        }
      }


Get Information About a Vehicle
```````````````````````````````

Returns detailed information about a vehicle.  This may include, but is not limitted to:

* Year
* Make
* Model
* Trim
* Engine Information
* Transmission Information
* Available Options


Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicle" : {
          "id" : "67e1e940-d6da-11e3-9c1a-0800200c9a66",
          "year" : "2007",
          "make" : "Toyota",
          "model" : "Camry",
          "trim" : "SE V6",
          "vin" : "2B4GP44R6WR942762",
          "data" : { ... },
          "links" : {
            "self" : "https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66"
          }
        }
      }


Transaction API
---------------

Get All Transactions for this Application
`````````````````````````````````````````

Returns a list of all transactions performed by this Application.

Results are returned in reverse-chronological order, i.e. time series order, using the "Stream Pagination" method.

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/transactions
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "transactions" : [
          {
            "id": "e7924989-e942-4ebb-a566-427984b91af1",
            "timestamp": "2015-06-22T00:30:19.455Z",
            "path": "/api/v1/devices?limit=1",
            "statusCode": 200,
            "method": "GET",
            "service": "vinli-platform-service"
          },
          {
            "id": "b7d746ce-1794-4796-9dc9-30ae091d1ce6",
            "timestamp": "2015-06-20T21:41:13.520Z",
            "path": "/api/v1/devices/c38ce5f2-0c4d-4d82-b301-fd87af5fcbd3/locations?limit=20",
            "service": "vinli-telemetry-service",
            "method": "GET",
            "statusCode": 200
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "remainingCount" : 1324,
            "limit" : 50,
            "until" : 1408945415426,
            "links" : {
              "latest" : "https://platform.vin.li/api/v1/transactions",
              "prior" : "https://platform.vin.li/api/v1/transactions?until=1408944636328"
            }
          }
        }
      }


Telemetry API
-------------
Get a List of Telemetry Messages
````````````````````````````````

Returns the latest `limit` number of telemetry messages that occurred before or at the `until` time and after the `since` time. If the `until` time is not specified, then the service will return snapshots until the current time when the call is made.

These messages are sent at least every five seconds and include the latest value of parameters captured by the Vinli device since the last message sent.


Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages
      Accept: application/json

* `until` - Results will contain snapshots whose timestamps are less than or equal to the `until` value. If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain snapshots whose timestamps are greater than the `since` value. If a `since` value is not specified, no lower limit will be placed on the returned snapshots.
* `limit` - Results will contain no more than `limit` number of snapshots


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "messages" : [
          {
            "id": "2f5f2a7c-02d8-4502-80c6-8cb52d9a08d5",
            "timestamp": "2014-07-14T17:46:06.759Z",
            "location": {
              "longitude": -90.0811,
              "latitude": 29.9508
            },
            "data" : {
              "vehicleSpeed": 12,
              "calculatedLoadValue": 34.5,
              "fuelType": "Gasoline",
              "rpm": 1254
            }
          },
          {
            "id": "b138303e-e40f-4d02-88a5-df41ca50ea3c",
            "timestamp": "2014-07-14T17:46:01.544Z",
            "location": {
              "longitude": -90.0813,
              "latitude": 29.950802
            },
            "data" : {
              "vehicleSpeed": 15,
              "rpm": 1766
            }
          },
          {
            "id": "fff266e2-deb3-4d3d-b181-bd0f048ce20c",
            "timestamp": "2014-07-14T17:45:54.872Z",
            "location": {
              "longitude": -90.08104,
              "latitude": 29.950813
            },
            "data" : {
              "vehicleSpeed": 16,
              "calculatedLoadValue": 56.3,
              "rpm": 1486
            }
          }
          ...
        ],
        "meta" : {
          "pagination" : {
            "remainingCount" : 1324,
            "limit" : 50,
            "until" : 1394733261450,
            "links" : {
              "latest" : "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages"
              "prior" : "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages?until=1394733251897"
            }
          }
        }
      }



Get a Specific Telemetry Message
````````````````````````````````

Returns a particular message by `messageId`. This is primarily used when a specific message is referenced by a different service.


Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/messages/2f11d630-141e-11e4-b717-5977b6c38d23
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message" : {
          "id" : "27a2ac50-d7bd-11e3-9c1a-0800200c9a66",
          "timestamp" : "2014-07-14T17:46:06.759Z",
          "location" : {
            "longitude" : -90.0811,
            "latitude" : 29.9508
          },
          "data" : {
            "vehicleSpeed": 12,
            "calculatedLoadValue": 34.5,
            "fuelType": "Gasoline",
            "rpm": 1254
          }
        }
      }

Locations
~~~~~~~~~

Returns the latest `limit` number of points of the device's location before or at the `until` time and after the `since` time. If the `until` time is not specified, then the service will return snapshots until the current time when the call is made. The `location` property contains a valid GeoJSON FeatureCollection object consisting of Point features for each location. The timestamp for each location is the in the `properties` field of the feature.

Additionally, selected or all parameters that were recorded at each location can also be included in the `properties` field. When `all` is specified, this method acts just like the Device Messages method below, but it is formatted as valid GeoJSON.


Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/locations?fields=rpm,vehicleSpeed
      Accept: application/json

* `fields` - Can be `all` or a comma-separated list of parameter keys to be included in the `properties` field.
* `until` - Results will contain snapshots whose timestamps are less than or equal to the `until` value. If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain snapshots whose timestamps are greater than the `since` value. If an `since` value is not specified, no lower limit will be placed on the returned snapshots.
* `limit` - Results will contain no more than `limit` number of snapshots


Response
++++++++

.. code-block:: json

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
          "pagination" : {
            "remaining" : 2341,
            "limit" : 200,
            "until" : 1394733260050,
            "links" : {
              "prior" : "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/locations?until=1394733247121"
            }
          }
        }
      }

Telemetry Snapshots
~~~~~~~~~~~~~~~~~~~

Returns the latest `limit` number of telemetry snapshots that contain at least one of the requested parameters that occurred before or at the `until` time and after the `since` time. If the `until` time is not specified, then the service will return snapshots until the current time when the call is made.

Request
+++++++

.. code-block:: json

      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType
      Accept: application/json

* `fields` - Comma-separated list of parameter keys to filter by
* `until` - Results will contain snapshots whose timestamps are less than or equal to the `until` value.  If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain snapshots whose timestamps are greater than the `since` value.  If a `since` value is not specified, no lower limit will be placed on the returned snapshots.
* `limit` - Results will contain no more than `limit` number of snapshots

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "snapshots": [
              {
                  "timestamp": 1394733260050,
                  "data": {
                      "vehicleSpeed": 12,
                      "calculatedLoadValue": 34.5,
                      "fuelType": "Gasoline"
                  }
              },
              {
                  "timestamp": 1394733255337,
                  "data": {
                      "vehicleSpeed": 15
                  }
              },
              {
                  "timestamp": 1394733251898,
                  "data": {
                      "rpm": 3827,
                      "calculatedLoadValue": 56.3
                  }
              }
          ],
          "meta": {
              "pagination": {
                  "remainingCount": 1324,
                  "limit": 50,
                  "until": 1394733261450,
                  "links": {
                      "latest": "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType",
                      "prior": "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?fields=rpm,vehicleSpeed,calculatedLoadValue,fuelType&until=1394733251897"
                  }
              }
          }
      }

Event API
---------
Get All Events for a Device
```````````````````````````

Returns the list all events for a given Device in reverse-chronological order.  Each Event contains information regarding the device, the object involved in the event, and associated metadata.

The following fields are contained within an event response:

* `id` - ID of the event
* `timestamp` - Timestamp when the event occurred
* `deviceId` - ID of the device
* `eventType` - Type of event
* `object` - Information about the object of the event (i.e. the associated Rule or Vehicle)
* `meta` - Optional data depending on the type of event.  For instance, for a `rule-enter` or `rule-leave` event, the `meta` property contains information about the Rule itself and the state and direction of the event.
* `links` - object containing links to associated data


Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events
      Accept: application/json


Parameters
++++++++++

* `type` - (optional) filter events for those of a given type
* `until` - Results will contain events whose timestamps are less than or equal to the `until` value. If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain events whose timestamps are greater than the `since` value. If an `since` value is not specified, no lower limit will be placed on the returned events.
* `limit` - Results will contain no more than `limit` number of events


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "events": [
              {
                  "id": "538f1195-a733-4ee7-a4e8-1fbbe7131f6a",
                  "timestamp": "2015-05-22T23:33:57.000Z",
                  "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                  "stored": "2015-05-22T23:33:58.741Z",
                  "storageLatency": 1741,
                  "eventType": "rule-leave",
                  "meta": {
                      "direction": "leave",
                      "firstEval": false,
                      "rule": {
                          "id": "429f9aa7-4c97-42c1-a459-ee1df6bc625b",
                          "name": "Speed Limit",
                          "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                          "boundaries": [
                              {
                                  "id": "0cadb0c8-a1c3-4176-86f2-20280ea72ad9",
                                  "type": "parametric",
                                  "parameter": "vehicleSpeed",
                                  "min": 48
                              }
                          ],
                          "evaluated": true,
                          "covered": false,
                          "createdAt": null,
                          "links": {
                              "self": "https://rules.vin.li/api/v1/rules/429f9aa7-4c97-42c1-a459-ee1df6bc625b"
                          }
                      },
                      "message": {
                          "id": "60afa670-d15b-4d2f-81bf-a068f4a9a7fb",
                          "timestamp": "2015-05-22T23:33:57.000Z",
                          "snapshot": {
                              "location": {
                                  "lat": 33.0246240995378,
                                  "lon": -97.0560955928522
                              },
                              "vehicleSpeed": 32
                          }
                      }
                  },
                  "object": {
                      "id": "429f9aa7-4c97-42c1-a459-ee1df6bc625b",
                      "type": "rule",
                      "appId": "b75afd8f-7247-46e6-a0f9-04f187c9d9bd"
                  },
                  "links": {
                      "self": "https://events.vin.li/api/v1/events/538f1195-a733-4ee7-a4e8-1fbbe7131f6a",
                      "notifications": "https://events.vin.li/api/v1/events/538f1195-a733-4ee7-a4e8-1fbbe7131f6a/notifications"
                  }
              },{
                  "id": "53bcdb2f-7a75-4225-ac15-b2d4364d9c7b",
                  "timestamp": "2015-05-22T18:25:43.000Z",
                  "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                  "stored": "2015-05-22T18:25:44.609Z",
                  "storageLatency": 1609,
                  "eventType": "startup",
                  "object": {
                      "id": "5956bc07-be98-4af5-91cc-86816aca7eb0",
                      "type": "vehicle"
                  },
                  "links": {
                      "self": "https://events.vin.li/api/v1/events/53bcdb2f-7a75-4225-ac15-b2d4364d9c7b",
                      "notifications": "https://events.vin.li/api/v1/events/53bcdb2f-7a75-4225-ac15-b2d4364d9c7b/notifications"
                  }
              }
          ],
          "meta": {
              "pagination": {
                  "remaining": 109,
                  "limit": 2,
                  "until": "2015-05-25T15:23:26.933Z",
                  "links": {
                      "prior": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events?until=2015-05-22T20%3A13%3A49.999Z"
                  }
              }
          }
      }


Get a Specific Event
````````````````````

Returns information about a specific event.


Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/events/538f1195-a733-4ee7-a4e8-1fbbe7131f6a
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "event": {
              "id": "538f1195-a733-4ee7-a4e8-1fbbe7131f6a",
              "timestamp": "2015-05-22T23:33:57.000Z",
              "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
              "stored": "2015-05-22T23:33:58.741Z",
              "storageLatency": 1741,
              "eventType": "rule-leave",
              "meta": {
                  "direction": "leave",
                  "firstEval": false,
                  "rule": {
                      "id": "429f9aa7-4c97-42c1-a459-ee1df6bc625b",
                      "name": "Speed Limit",
                      "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                      "boundaries": [
                          {
                              "id": "0cadb0c8-a1c3-4176-86f2-20280ea72ad9",
                              "type": "parametric",
                              "parameter": "vehicleSpeed",
                              "min": 48
                          }
                      ],
                      "evaluated": true,
                      "covered": false,
                      "createdAt": null,
                      "links": {
                          "self": "https://rules.vin.li/api/v1/rules/429f9aa7-4c97-42c1-a459-ee1df6bc625b"
                      }
                  },
                  "message": {
                      "id": "60afa670-d15b-4d2f-81bf-a068f4a9a7fb",
                      "timestamp": "2015-05-22T23:33:57.000Z",
                      "snapshot": {
                          "location": {
                              "lat": 33.0246240995378,
                              "lon": -97.0560955928522
                          },
                          "vehicleSpeed": 32
                      }
                  }
              },
              "object": {
                  "id": "429f9aa7-4c97-42c1-a459-ee1df6bc625b",
                  "type": "rule",
                  "appId": "b75afd8f-7247-46e6-a0f9-04f187c9d9bd"
              },
              "links": {
                  "self": "https://events.vin.li/api/v1/events/538f1195-a733-4ee7-a4e8-1fbbe7131f6a",
                  "notifications": "https://events.vin.li/api/v1/events/538f1195-a733-4ee7-a4e8-1fbbe7131f6a/notifications"
              }
          }
      }


Subscriptions
~~~~~~~~~~~~~

In order to receive notification for vehicle events, your application must subscribe to events for each device individually.

Each Subscription relates to a given event or class of events from a given Device and specifies the external URL that will be called when the event occurs and any additional "App Data" that should be included.


Notification Payload
````````````````````

When a subscription is triggered, an HTTP call using the "POST" method is made to the Subscription's URL.  This call uses content-type of "application/json" and sends a JSON representation containing a `notification` root object along with representations of the Event that triggered the notification and the associated Subscription:

.. code-block:: json

      {
          "notification": {
              "event": {
                  "id": "314d7fcd-d4d6-4b78-9804-b171db60790a",
                  "timestamp": "2015-06-16T13:12:34.000Z",
                  "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
                  "eventType": "rule-leave",
                  "object": {
                      "id": "79f2e013-b6b9-44dd-9f34-4be5da971d7a",
                      "type": "rule",
                      "appId": "b75afd8f-7247-46e6-a0f9-04f187c9d9bd"
                  },
                  "meta": {
                      "direction": "leave",
                      "firstEval": false,
                      "rule": {
                          "id": "79f2e013-b6b9-44dd-9f34-4be5da971d7a",
                          "name": "My Geofence",
                          "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
                          "boundaries": [],
                          "evaluated": true,
                          "covered": false,
                          "createdAt": "2015-06-16T12:54:09.601Z",
                          "links": {
                              "self": "https://rules.vin.li/api/v1/rules/79f2e013-b6b9-44dd-9f34-4be5da971d7a",
                              "events": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/events?type=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a",
                              "subscriptions": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/subscriptions?objectType=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a"
                          }
                      },
                      "message": {
                          "id": "cd339f3d-b0d8-49a9-a87d-ca7ee3a937e2",
                          "timestamp": "2015-06-16T13:12:34.000Z",
                          "snapshot": {
                              "location": {
                                  "lat": 32.5536468870112,
                                  "lon": -96.1153222519258
                              }
                          }
                      }
                  }
              },
              "subscription": {
                  "id": "a896ff7d-ca46-4bf4-af71-b9b1573c3ef1",
                  "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
                  "eventType": "rule-leave",
                  "url": "https://myapp.com/notifications",
                  "object": {
                      "id": "79f2e013-b6b9-44dd-9f34-4be5da971d7a",
                      "type": "rule"
                  },
                  "appData": "{\"message\":\"This is your app-specific data\"}"
              }
          }
      }

Note that the `appData` attribute of the `subscription` property contains the Application-specific data that you created the Subscription with, if applicable.

In the example above, the Subscription triggered is associated with a Rule.  In this case, additional information is made available in the Notificaiton including a reprsentation of the Rule in the `meta` property.  Additionally, a very useful property `firstEval` is provided that lets your Application know whether or not this is the first evaluation of the Rule.  The first evaluation of a Rule in which it can be established that the device is covered or not covered by the boundaries will always result in a notification.  Using the `firstEval` property, your App can determine if the device was previously in a different state or was just in an unknown state.


Create a Subscription
`````````````````````

A Subscription must include, at a minimum an `eventType` and a `url`.  Additionally, if the subscription references a given Rule, it must be included in the `object`.

Request
+++++++

.. code-block:: json

      POST https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions
      Accept: application/json
      Content-Type: application/json

      {
        "subscription" : {
          "eventType" : "startup",
          "url": "https://myapp.com/notifications"
        }
      }


Response
++++++++

.. code-block:: json

      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://events.vin.li/api/v1/subscriptions/77965f0f-d468-48e1-9585-69d547900058

      {
          "subscription" : {
              "id": "77965f0f-d468-48e1-9585-69d547900058",
              "deviceId": "de01abb1-453d-4293-831a-f0d804b48fdf",
              "eventType": "startup",
              "url": "https://myapp.com/notifications",
              "createdAt": "2015-06-16T12:54:09.876Z",
              "updatedAt": "2015-06-16T12:54:09.876Z",
              "links": {
                  "self": "https://events.vin.li/api/v1/subscriptions/77965f0f-d468-48e1-9585-69d547900058",
                  "notifications": "https://events.vin.li/api/v1/subscriptions/77965f0f-d468-48e1-9585-69d547900058/notifications"
              }
          }
      }


When creating a Subscription to a Rule's events, identification of the Rule is required.  An application can only subscribe to Rule events for Rules to which it has access.  A special eventType (`rule-*`) can be used to subscribe to both `rule-enter` and `rule-leave` events.

Also note that in the example below, `appData` is given so that this is passed on to the App whenever the subscription is triggered.


Request
+++++++

.. code-block:: json

      POST https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions
      Accept: application/json
      Content-Type: application/json

      {
        "subscription" : {
          "eventType" : "rule-*",
          "url": "https://myapp.com/notifications",
          "appData": "{\"message\":\"This is your app-specific data\"}",
          "object": {
              "id": "41d68c9e-2914-4923-8593-3abdf299537c",
              "type": "rule"
          }
        }
      }


Response
++++++++

.. code-block:: json

      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b

      {
          "subscription" : {
              "id": "917fb546-5666-4fdd-aed6-53fa099b313b",
              "deviceId": "de01abb1-453d-4293-831a-f0d804b48fdf",
              "eventType": "rule-*",
              "object": {
                  "id": "58f815b9-693d-450a-8814-779c9bf8ad6f",
                  "type": "rule"
              },
              "url": "https://myapp.com/notifications",
              "appData": "{\"message\":\"This is your app-specific data\"}"
              "createdAt": "2015-06-16T12:54:09.876Z",
              "updatedAt": "2015-06-16T12:54:09.876Z",
              "links": {
                  "self": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b",
                  "notifications": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b/notifications"
              }
          }
      }



Get all Subscriptions for a Device
``````````````````````````````````

Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "subscriptions": [
              {
                  "id": "917fb546-5666-4fdd-aed6-53fa099b313b",
                  "deviceId": "de01abb1-453d-4293-831a-f0d804b48fdf",
                  "eventType": "rule-*",
                  "object": {
                      "id": "58f815b9-693d-450a-8814-779c9bf8ad6f",
                      "type": "rule"
                  },
                  "url": "https://myapp.com/notifications",
                  "appData": "{\"message\":\"This is your app-specific data\"}"
                  "createdAt": "2015-06-16T12:54:09.876Z",
                  "updatedAt": "2015-06-16T12:54:09.876Z",
                  "links": {
                      "self": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b",
                      "notifications": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b/notifications"
                  }
              },
              ...
          ],
          "meta": {
              "pagination": {
                  "total": 70,
                  "limit": 20,
                  "offset": 0,
                  "links": {
                      "first": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions?offset=0&limit=20",
                      "last": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions?offset=60&limit=20",
                      "next": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions?offset=20&limit=20"
                  }
              }
          }
      }


Get a Specific Subscription
```````````````````````````

Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "subscription": {
              "id": "917fb546-5666-4fdd-aed6-53fa099b313b",
              "deviceId": "de01abb1-453d-4293-831a-f0d804b48fdf",
              "eventType": "rule-*",
              "object": {
                  "id": "58f815b9-693d-450a-8814-779c9bf8ad6f",
                  "type": "rule"
              },
              "url": "https://myapp.com/notifications",
              "appData": "{\"message\":\"This is your app-specific data\"}"
              "createdAt": "2015-06-16T12:54:09.876Z",
              "updatedAt": "2015-06-16T12:54:09.876Z",
              "links": {
                  "self": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b",
                  "notifications": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b/notifications"
              }
          }
      }


Update a Subscription
`````````````````````

Subscriptions are primarily immutable.  The `url` and `appData` properties can be updated; however, the "functional" parts of the Subscription (`eventType`, `object`, etc.) are not modifiable.


Request
+++++++

.. code-block:: json

      POST https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions
      Accept: application/json
      Content-Type: application/json

      {
        "subscription" : {
          "url": "https://myapp.com/v2/notifications",
          "appData": "{\"message\":\"This is updated app-specific data\"}",
        }
      }


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "subscription" : {
              "id": "917fb546-5666-4fdd-aed6-53fa099b313b",
              "deviceId": "de01abb1-453d-4293-831a-f0d804b48fdf",
              "eventType": "rule-*",
              "object": {
                  "id": "58f815b9-693d-450a-8814-779c9bf8ad6f",
                  "type": "rule"
              },
              "url": "https://myapp.com/v2/notifications",
              "appData": "{\"message\":\"This is updated app-specific data\"}",
              "createdAt": "2015-06-16T12:54:09.876Z",
              "updatedAt": "2015-06-16T12:54:09.876Z",
              "links": {
                  "self": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b",
                  "notifications": "https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b/notifications"
              }
          }
      }


Delete a Subscription
`````````````````````

Request
+++++++

.. code-block:: json

      DELETE https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT



Notifications
~~~~~~~~~~~~~

Each time a subscription is triggered by an event, a new Notification is created that represents the event, subscription, and subsequent actions taken by the Vinli platform to notify your application.

Notification state is useful in debugging notification handlers on your App.  This `state`, `responseCode`, and `response` properties will inform you as to the result of Event Services' attempt to call the notification URL.  A notification will be linked to one subscription and may contain additional metadata depending on the trigger of the subscription.  In the case of subscriptions to Rules, this metadata

Fields included in a notification response include:

* `id` - ID of the notification
* `eventId` - ID of the event that triggered the notification
* `eventType` - Type of the associated event
* `eventTimestamp` - Time that the associated event occurred
* `subscriptionId` - ID of the subscription that this notification is associated with
* `url` - URL that was called by Event Service; this is copied from the subscription at the creation of the notification
* `payload` - String of the payload exactly as it was posted to the above URL
* `state` - Current state of the notification.  State values may include `created`, `queued`, `complete`, or `error`

The `state` of a notification start as  `created` and moves to `queued` as soon as it is placed in the notification queue to be processed.  Once the notification has been posted to the callback URL, the state will be moved to `complete` if the HTTP transaction was completed and a response code in the 200s was received.  If the HTTP call is not able to be completed or a response code other than the 200s, the state will become `error`.

If the notification is in the `complete` or `error` state, the fields below will be available in the response:

* `responseCode` - HTTP code received from the URL above
* `response` - String of the response from the URL above
* `notifiedAt` - Time that the HTTP call was initiated
* `respondedAt` - Time that the HTTP call was completed (if successful)

Get a Specific Notification
```````````````````````````

Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/notifications/09704b59-83d9-44a5-a0f8-33d973bdac5e
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "notification": {
              "id": "09704b59-83d9-44a5-a0f8-33d973bdac5e",
              "eventId": "314d7fcd-d4d6-4b78-9804-b171db60790a",
              "eventType": "rule-leave",
              "eventTimestamp": "2015-06-16T13:12:34.000Z",
              "subscriptionId": "a896ff7d-ca46-4bf4-af71-b9b1573c3ef1",
              "state": "complete",
              "responseCode": 201,
              "response": "{\"status\":\"success\"}",
              "url": "https://myapp.com/notifications",
              "payload": "{\"notification\":{\"event\":{\"id\":\"314d7fcd-d4d6-4b78-9804-b171db60790a\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"stored\":\"2015-06-16T13:12:35.825Z\",\"storageLatency\":1825,\"eventType\":\"rule-leave\",\"meta\":{\"direction\":\"leave\",\"firstEval\":false,\"rule\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"name\":\"[geofence] Marlee\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"boundaries\":[],\"evaluated\":true,\"covered\":false,\"createdAt\":\"2015-06-16T12:54:09.601Z\",\"links\":{\"self\":\"https://rules.vin.li/api/v1/rules/79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"events\":\"https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/events?type=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"subscriptions\":\"https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/subscriptions?objectType=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a\"}},\"message\":{\"id\":\"cd339f3d-b0d8-49a9-a87d-ca7ee3a937e2\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"snapshot\":{\"location\":{\"lat\":32.5536468870112,\"lon\":-96.1153222519258}}}},\"object\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"type\":\"rule\",\"appId\":\"b75afd8f-7247-46e6-a0f9-04f187c9d9bd\"}},\"subscription\":{\"id\":\"a896ff7d-ca46-4bf4-af71-b9b1573c3ef1\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"eventType\":\"rule-leave\",\"url\":\"https://myapp.com/notifications\",\"object\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"type\":\"rule\"},\"appData\":\"{\\\"message\\\":\\\"This is your app-specific data\\\"}\"}}}",
              "notifiedAt": "2015-06-16T13:12:35.862Z",
              "respondedAt": "2015-06-16T13:12:36.300Z",
              "createdAt": "2015-06-16T13:12:35.842Z",
              "links": {
                  "self": "https://events.vin.li/api/v1/notifications/09704b59-83d9-44a5-a0f8-33d973bdac5e",
                  "event": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/events/314d7fcd-d4d6-4b78-9804-b171db60790a",
                  "subscription": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/subscriptions/a896ff7d-ca46-4bf4-af71-b9b1573c3ef1"
              }
          }
      }

Get Notifications for a Subscription
````````````````````````````````````

Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/subscriptions/a896ff7d-ca46-4bf4-af71-b9b1573c3ef1/notifications
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "notifications": [
              {
                  "id": "09704b59-83d9-44a5-a0f8-33d973bdac5e",
                  "eventId": "314d7fcd-d4d6-4b78-9804-b171db60790a",
                  "eventType": "rule-leave",
                  "eventTimestamp": "2015-06-16T13:12:34.000Z",
                  "subscriptionId": "a896ff7d-ca46-4bf4-af71-b9b1573c3ef1",
                  "state": "complete",
                  "responseCode": 201,
                  "response": "{\"status\":\"success\"}",
                  "url": "https://myapp.com/notifications",
                  "payload": "{\"notification\":{\"event\":{\"id\":\"314d7fcd-d4d6-4b78-9804-b171db60790a\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"stored\":\"2015-06-16T13:12:35.825Z\",\"storageLatency\":1825,\"eventType\":\"rule-leave\",\"meta\":{\"direction\":\"leave\",\"firstEval\":false,\"rule\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"name\":\"[geofence] Marlee\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"boundaries\":[],\"evaluated\":true,\"covered\":false,\"createdAt\":\"2015-06-16T12:54:09.601Z\",\"links\":{\"self\":\"https://rules.vin.li/api/v1/rules/79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"events\":\"https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/events?type=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"subscriptions\":\"https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/subscriptions?objectType=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a\"}},\"message\":{\"id\":\"cd339f3d-b0d8-49a9-a87d-ca7ee3a937e2\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"snapshot\":{\"location\":{\"lat\":32.5536468870112,\"lon\":-96.1153222519258}}}},\"object\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"type\":\"rule\",\"appId\":\"b75afd8f-7247-46e6-a0f9-04f187c9d9bd\"}},\"subscription\":{\"id\":\"a896ff7d-ca46-4bf4-af71-b9b1573c3ef1\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"eventType\":\"rule-leave\",\"url\":\"https://myapp.com/notifications\",\"object\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"type\":\"rule\"},\"appData\":\"{\\\"message\\\":\\\"This is your app-specific data\\\"}\"}}}",
                  "notifiedAt": "2015-06-16T13:12:35.862Z",
                  "respondedAt": "2015-06-16T13:12:36.300Z",
                  "createdAt": "2015-06-16T13:12:35.842Z",
                  "links": {
                      "self": "https://events.vin.li/api/v1/notifications/09704b59-83d9-44a5-a0f8-33d973bdac5e",
                      "event": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/events/314d7fcd-d4d6-4b78-9804-b171db60790a",
                      "subscription": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/subscriptions/a896ff7d-ca46-4bf4-af71-b9b1573c3ef1"
                  }
              }
          ],
          "meta": {
              "pagination": {
                  "total": 1,
                  "limit": 20,
                  "offset": 0,
                  "links": {
                      "first": "https://events.vin.li/api/v1/subscriptions/a896ff7d-ca46-4bf4-af71-b9b1573c3ef1/notifications?offset=0&limit=20",
                      "last": "https://events.vin.li/api/v1/subscriptions/a896ff7d-ca46-4bf4-af71-b9b1573c3ef1/notifications?offset=0&limit=20"
                  }
              }
          }
      }



Get Notifications for an Event
``````````````````````````````

Returns the notifications that were triggered for any subscription associated with a given event.


Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/events/314d7fcd-d4d6-4b78-9804-b171db60790a/notifications
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "notifications": [
              {
                  "id": "09704b59-83d9-44a5-a0f8-33d973bdac5e",
                  "eventId": "314d7fcd-d4d6-4b78-9804-b171db60790a",
                  "eventType": "rule-leave",
                  "eventTimestamp": "2015-06-16T13:12:34.000Z",
                  "subscriptionId": "a896ff7d-ca46-4bf4-af71-b9b1573c3ef1",
                  "state": "complete",
                  "responseCode": 201,
                  "response": "{\"status\":\"success\"}",
                  "url": "https://myapp.com/notifications",
                  "payload": "{\"notification\":{\"event\":{\"id\":\"314d7fcd-d4d6-4b78-9804-b171db60790a\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"stored\":\"2015-06-16T13:12:35.825Z\",\"storageLatency\":1825,\"eventType\":\"rule-leave\",\"meta\":{\"direction\":\"leave\",\"firstEval\":false,\"rule\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"name\":\"[geofence] Marlee\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"boundaries\":[],\"evaluated\":true,\"covered\":false,\"createdAt\":\"2015-06-16T12:54:09.601Z\",\"links\":{\"self\":\"https://rules.vin.li/api/v1/rules/79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"events\":\"https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/events?type=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"subscriptions\":\"https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/subscriptions?objectType=rule&objectId=79f2e013-b6b9-44dd-9f34-4be5da971d7a\"}},\"message\":{\"id\":\"cd339f3d-b0d8-49a9-a87d-ca7ee3a937e2\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"snapshot\":{\"location\":{\"lat\":32.5536468870112,\"lon\":-96.1153222519258}}}},\"object\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"type\":\"rule\",\"appId\":\"b75afd8f-7247-46e6-a0f9-04f187c9d9bd\"}},\"subscription\":{\"id\":\"a896ff7d-ca46-4bf4-af71-b9b1573c3ef1\",\"deviceId\":\"4bffefbb-9fba-43ee-aebe-ed7f7f2fae84\",\"eventType\":\"rule-leave\",\"url\":\"https://myapp.com/notifications\",\"object\":{\"id\":\"79f2e013-b6b9-44dd-9f34-4be5da971d7a\",\"type\":\"rule\"},\"appData\":\"{\\\"message\\\":\\\"This is your app-specific data\\\"}\"}}}",
                  "notifiedAt": "2015-06-16T13:12:35.862Z",
                  "respondedAt": "2015-06-16T13:12:36.300Z",
                  "createdAt": "2015-06-16T13:12:35.842Z",
                  "links": {
                      "self": "https://events.vin.li/api/v1/notifications/09704b59-83d9-44a5-a0f8-33d973bdac5e",
                      "event": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/events/314d7fcd-d4d6-4b78-9804-b171db60790a",
                      "subscription": "https://events.vin.li/api/v1/devices/4bffefbb-9fba-43ee-aebe-ed7f7f2fae84/subscriptions/a896ff7d-ca46-4bf4-af71-b9b1573c3ef1"
                  }
              }
          ],
          "meta": {
              "pagination": {
                  "total": 1,
                  "limit": 20,
                  "offset": 0,
                  "links": {
                      "first": "https://events.vin.li/api/v1/events/314d7fcd-d4d6-4b78-9804-b171db60790a/notifications?offset=0&limit=20",
                      "last": "https://events.vin.li/api/v1/events/314d7fcd-d4d6-4b78-9804-b171db60790a/notifications?offset=0&limit=20"
                  }
              }
          }
      }


Diagnostic API
--------------

Device DTC  Service
~~~~~~~~~~~~~~~~~~~

List all DTC Codes for a Device
``````````````````````````````````````````

The DTC History Service provides historical information for DTC codes for a given vehicle.  Each time a new DTC code is seen, it triggers a DTC Event.  These events either resolve when the DTC code is no longer seen or remain "open" until the code is resolved.

Request
+++++++

.. code-block:: json

      GET https://diagnostics.vin.li/api/v1/vehicles/47fa348e-c3fa-4cad-8272-61940eae7748/codes
      Accept: application/json

The state query param may be used to filter the response. Valid values are active and inactive. These will filter the response to only include either DTC codes that are still on presently or not. The absence of the state query param will not filter the response and so the response will contain the full history DTC codes.

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "codes" : [
          {
            "id" : "86273a41-2d5a-427b-bfb8-474b73bace14",
            "deviceId" : "bc6825db-716a-47ae-9eb1-8752af83361d",
            "vehicleId" : "2594b0b5-0d9f-463a-b4e6-4eadc20bec49",
            "number" : "P0152",
            "start" : "2014-09-06T03:09:34.957Z",
            "stop" : null,
            "links" : {
              "device" : "https://platform.vin.li/api/v1/devices/bc6825db-716a-47ae-9eb1-8752af83361d",
              "vehicle" : "https://platform.vin.li/api/v1/devices/2594b0b5-0d9f-463a-b4e6-4eadc20bec49"
            }
          },
          {
            "id" : "b943019b-b0ab-4350-9595-5c09f79f18ed",
            "deviceId" : "bc6825db-716a-47ae-9eb1-8752af83361d",
            "vehicleId" : "2594b0b5-0d9f-463a-b4e6-4eadc20bec49",
            "number" : "P0135",
            "start" : "2014-09-06T03:09:34.957Z",
            "stop" : "2014-09-06T03:10:14.384Z",
            "links" : {
              "device" : "https://platform.vin.li/api/v1/devices/bc6825db-716a-47ae-9eb1-8752af83361d",
              "vehicle" : "https://platform.vin.li/api/v1/devices/2594b0b5-0d9f-463a-b4e6-4eadc20bec49"
            }
          },
          {
            "id": "429d0c42-381b-499c-bd6c-4a5620e6b1ed",
            "deviceId": "bc6825db-716a-47ae-9eb1-8752af83361d",
            "vehicleId": "2594b0b5-0d9f-463a-b4e6-4eadc20bec49",
            "number" : "P0171",
            "start" : "2014-09-05T12:05:46.893Z",
            "stop" : "2014-09-06T03:10:14.384Z",
            "links" : {
              "device" : "https://platform.vin.li/api/v1/devices/bc6825db-716a-47ae-9eb1-8752af83361d",
              "vehicle" : "https://platform.vin.li/api/v1/devices/2594b0b5-0d9f-463a-b4e6-4eadc20bec49"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "remaining": 0,
            "until": "2015-07-24T23:00:40.683Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 20,
            "sortDir": "desc",
            "links" : {}
          }
        }
      }

DTC Info Service
~~~~~~~~~~~~~~~~

Get DTC Code Information
````````````````````````````````

There's a lot of information encoded in the DTC codes reported by a Vehicle.  This method is meant to provide this information for a given DTC code so that your Application can present useful information to the end-user.

Request
+++++++

.. code-block:: json

      GET https://diagnostics.vin.li/api/v1/codes?number=P0171
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "code" : {
          "make": "generic",
          "twoByte": {
            "number": "P0001",
            "description": "Fuel Volume Regulator Control Circuit/Open"
          },
          "threeByte": {
            "number": "P0001",
            "ftb": "13",
            "fault": "Circuit Open",
            "description": "Fuel Volume Regulator Control"
          }
        }
      }

Trip API
--------

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

Please note, that trips are sometimes created asynchronously--either because they have to be constructed by post-processing or after bulk data upload for a given device.


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
            "self": "https://trips.vin.li/api/v1/trips/a51a3c87-baa7-4e5d-98e6-4f9588d7c2e1",
            "device": "https://platform.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicle": "https://platform.vin.li/api/v1/vehicles/0c785aa0-1a48-4cc6-9f5c-028350dd907d",
            "locations": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/locations?since=1440012315951&until=1440012928875",
            "messages": "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/messages?since=1440012315951&until=1440012928875",
            "events": "https://events.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/events?since=1440012315951&until=1440012928875"
          }
        }
      }

Behavioral API
------------------
Report Cards for a Device
```````````````````````````````

Returns a Report Card based on historical data for a specified period. In some cases, not enough information was gathered to generate a Report Card.  In these cases, the grades will be reported as "I" (for "Incomplete" to keep the school report card metaphore going).

Request
+++++++

.. code-block:: json

      GET https://behavior.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/report_cards
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "reportCards" : [
          {
            "id": "549d628c-48dc-412d-8087-44a9f82f187e",
            "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicleId": "ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55",
            "tripId": "b9e58eb4-0743-45e9-b9c6-86500f5412bb",
            "grade": "A",
            "links": {
              "self": "https://behavioral.vin.li/api/v1/report_cards/549d628c-48dc-412d-8087-44a9f82f187e",
              "trip": "https://trips.vin.li/api/v1/trips/b9e58eb4-0743-45e9-b9c6-86500f5412bb",
              "device": "https://platform.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
              "vehicle": "https://platform.vin.li/api/v1/vehicles/ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55"
            }
          }
        ],
        "meta": {
          "pagination": {
            "remaining": 34,
            "until": "2015-08-13T22:20:59.330Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 20,
            "sortDir": "desc",
            "links": {
              "prior": "https://behavioral-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58/report_cards?until=1439418498459"
            }
          }
        }
      }



Lifetime Report Card for a Device
`````````````````````````````````

Returns a Report Card based on all historical data available for a given Device.

Request
+++++++

.. code-block:: json

      GET https://behavior.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/report_cards/overall
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "reportCard": {
           "overallGrade": "A"
        }
      }


Report Card for a Trip
``````````````````````

The Trip-specific Report Card contains the same data as the Long-Term and Lifetime Report Card but is specific for a particular Trip.

In some cases, the Trip is too short to generate the data necessary for the Report Card analysis to be run.  In these cases, the grades will be reported as "I".

Request
+++++++

.. code-block:: json

      GET https://behavior.vin.li/api/v1/trips/b9e58eb4-0743-45e9-b9c6-86500f5412bb/report_card
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "reportCards" : [
          {
            "id": "549d628c-48dc-412d-8087-44a9f82f187e",
            "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicleId": "ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55",
            "tripId": "b9e58eb4-0743-45e9-b9c6-86500f5412bb",
            "grade": "I",
            "links": {
              "self": "https://behavioral.vin.li/api/v1/report_cards/549d628c-48dc-412d-8087-44a9f82f187e",
              "trip": "https://trips.vin.li/api/v1/trips/b9e58eb4-0743-45e9-b9c6-86500f5412bb",
              "device": "https://platform.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
              "vehicle": "https://platform.vin.li/api/v1/vehicles/ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55"
            }
          }
        ]
      }

Safety API
----------
Get a list of Collisions for a Device
`````````````````````````````````````

Returns a list of registered Collisions for a given device.

Request
+++++++

.. code-block:: json

      GET https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/collisions
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "collisions" : [
          {
            "id" : "561f0fa0-3231-11e4-8c21-0800200c9a66",
            "timestamp" : "2015-07-05T22:16:18+00:00",
            "location" : {
              "latitude" : 32.766392,
              "longitude" : -96.917009
            },
            "links" : {
              "self" : "https://safety.vin.li/api/v1/collisions/561f0fa0-3231-11e4-8c21-0800200c9a66"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "total" : 22,
            "offset" : 0,
            "limit" : 20,
            "links" : {
              "first" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/collisions?offset=0&limit=20",
              "last" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/collisions?offset=20&limit=20",
              "next" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/collisions?offset=20&limit=20"
            }
          }
        }
      }



Get a list of Collisions for a Vehicle
``````````````````````````````````````

Returns a list of registered Collisions for a given Vehicle.

Request
+++++++

.. code-block:: json

      GET https://safety.vin.li/api/v1/vehicles/e619dc1d-b760-410f-b809-2578df22a755/collisions
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "collisions" : [
          {
            "id" : "561f0fa0-3231-11e4-8c21-0800200c9a66",
            "timestamp" : "2015-07-05T22:16:18+00:00",
            "location" : {
              "latitude" : 32.766392,
              "longitude" : -96.917009
            },
            "links" : {
              "self" : "https://safety.vin.li/api/v1/collisions/561f0fa0-3231-11e4-8c21-0800200c9a66"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "total" : 22,
            "offset" : 0,
            "limit" : 20,
            "links" : {
              "first" : "https://safety.vin.li/api/v1/vehicles/e619dc1d-b760-410f-b809-2578df22a755/collisions?offset=0&limit=20",
              "last" : "https://safety.vin.li/api/v1/vehicles/e619dc1d-b760-410f-b809-2578df22a755/collisions?offset=20&limit=20",
              "next" : "https://safety.vin.li/api/v1/vehicles/e619dc1d-b760-410f-b809-2578df22a755/collisions?offset=20&limit=20"
            }
          }
        }
      }

Get a specific Collision
````````````````````````

Returns a list of registered Collisions for a given Vehicle.

Request
+++++++

.. code-block:: json

      GET https://safety.vin.li/api/v1/collisions/e43ff87d-bb58-42da-998e-d7f10a3f7a64
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "collision" : {
          "id" : "e43ff87d-bb58-42da-998e-d7f10a3f7a64",
          "timestamp" : "2015-07-05T22:16:18+00:00",
          "location" : {
            "latitude" : 32.766392,
            "longitude" : -96.917009
          },
          "links" : {
            "self" : "https://safety.vin.li/api/v1/collisions/e43ff87d-bb58-42da-998e-d7f10a3f7a64"
          }
        }
      }

