Events
-------

Get All Events for a Device
`````````````````````````````

Returns the list all events for a given Device in reverse-chronological order.  Each Event contains information regarding the device, the object involved in the event, and associated metadata.

The following fields are contained within an event response:

* `id` - ID of the event
* `timestamp` - Timestamp when the event occurred
* `deviceId` - ID of the device
* `vehicleId` - ID of the vehicle
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
                  "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
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
                  "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
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


Get All Events for a Vehicle
`````````````````````````````


Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/vehicles/48ef1264-7fd2-4319-8789-g9a6b85b7a8f/events
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "events": [
          {
            "id": "c0c19d22-0f59-4140-9076-c61f61740f76",
            "timestamp": "2016-10-20T17:29:48.753Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "trip-completed",
            "object": {
              "id": "310d9507-deae-437c-a18c-4b7909173939",
              "type": "trip"
            },
            "meta": {
              "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f"
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/c0c19d22-0f59-4140-9076-c61f61740f76",
              "notifications": "https://events.vin.li/api/v1/events/c0c19d22-0f59-4140-9076-c61f61740f76/notifications"
            }
          },
          {
            "id": "a5c98193-d845-4898-b69a-2f735aa4bfc3",
            "timestamp": "2016-10-20T17:29:44.204Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "shutdown",
            "object": {
              "id": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
              "type": "vehicle"
            },
            "meta": null,
            "links": {
              "self": "https://events.vin.li/api/v1/events/a5c98193-d845-4898-b69a-2f735aa4bfc3",
              "notifications": "https://events.vin.li/api/v1/events/a5c98193-d845-4898-b69a-2f735aa4bfc3/notifications"
            }
          },
          {
            "id": "7933c50a-e422-3ff9-v51d-cddc443f1a88",
            "timestamp": "2016-10-20T14:00:19.547Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "rule-leave",
            "object": {
              "id": "6cf4ddaa-3c16-439c-bc3f-6bb9a7dcb7fd",
              "type": "rule"
            },
            "meta": {
              "direction": "leave",
              "firstEval": false,
              "rule": {
                "id": "6cf4ddaa-3c16-439c-bc3f-6bb9a7dcb7fd",
                "name": "new geofence",
                "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                "boundaries": [
                  {
                    "id": "5714379f-c5f3-4052-ad5d-0aa22032475b",
                    "type": "radius",
                    "radius": 312.33,
                    "lon": -96.7899370193481,
                    "lat": 32.8242218079282
                  }
                ],
                "evaluated": true,
                "covered": false,
                "createdAt": "2016-07-23T05:41:28.179+00:00",
                "links": {
                  "self": "https://rules.vin.li/api/v1/rules/6cf4ddaa-3c16-439c-bc3f-6bb9a7dcb7fd",
                  "events": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events?type=rule-*&objectId=6cf4ddaa-3c16-439c-bc3f-6bb9a7dcb7fd",
                  "subscriptions": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/subscriptions?objectType=rule&objectId=6cf4ddaa-3c16-439c-bc3f-6bb9a7dcb7fd"
                }
              },
              "message": {
                "id": "645ff3f0-c8a9-4538-b903-2a8b29087635",
                "timestamp": "2016-10-20T14:00:19.547Z",
                "snapshot": {
                  "location": {
                    "lat": 41.502994,
                    "lon": -71.314856
                  },
                  "accel": {
                    "maxZ": -4.137202,
                    "maxX": 1.379067,
                    "maxY": -5.439654,
                    "minX": 0.229845,
                    "minY": -8.236096,
                    "minZ": -6.473954
                  },
                  "massAirFlow": 18.69,
                  "rpm": 1802,
                  "vehicleSpeed": 13,
                  "intakeManifoldPressure": 60,
                  "fuelAirCommandedEquivalenceRatio": 0.973236083984375
                }
              }
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/7933c50a-e422-3ff9-v51d-cddc443f1a88",
              "notifications": "https://events.vin.li/api/v1/events/7933c50a-e422-3ff9-v51d-cddc443f1a88/notifications"
            }
          }
        ],
        "meta": {
          "pagination": {
            "remaining": 1214,
            "until": "2016-10-20T18:09:29.977Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 20,
            "sortDir": "desc",
            "links": {
              "prior": "https://events.vin.li/api/v1/vehicles/48ef1264-7fd2-4319-8789-g9a6b85b7a8f/events?until=1476971981756"
            }
          }
        }
      }


Get a Specific Event
`````````````````````

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
              "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
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
