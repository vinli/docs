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

* `type` - (optional) filter events for those of a given `eventType`
* `until` - Results will contain events whose timestamps are less than or equal to the `until` value. If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain events whose timestamps are greater than the `since` value. If an `since` value is not specified, no lower limit will be placed on the returned events.
* `limit` - Results will contain no more than `limit` number of events. Defaults to 20.


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "events": [
          {
            "id": "5dd7722c-58e2-4f66-9636-e57dd829abbe",
            "timestamp": "2016-12-20T17:44:09.187Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "trip-completed",
            "object": {
              "id": "1b8b9447-428c-4c0d-631d-1bc27b401c15",
              "type": "trip"
            },
            "meta": {
              "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f"
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/5dd7722c-58e2-4f66-9636-e57dd829abbe",
              "notifications": "https://events.vin.li/api/v1/events/5dd7722c-58e2-4f66-9636-e57dd829abbe/notifications"
            }
          },
          {
            "id": "0e9a17ff-6f81-436f-9686-2f517928fe65",
            "timestamp": "2016-12-20T17:44:04.587Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "trip-stopped",
            "object": {
              "id": "1b8b9447-428c-4c0d-631d-1bc27b401c15",
              "type": "trip"
            },
            "meta": {
              "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f"
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/0e9a17ff-6f81-436f-9686-2f517928fe65",
              "notifications": "https://events.vin.li/api/v1/events/0e9a17ff-6f81-436f-9686-2f517928fe65/notifications"
            }
          },
          {
            "id": "49f0f996-ace4-4fb2-bcd1-be1ae4979866",
            "timestamp": "2016-12-20T17:44:04.587Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "shutdown",
            "object": {
              "id": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
              "type": "vehicle"
            },
            "meta": null,
            "links": {
              "self": "https://events.vin.li/api/v1/events/49f0f996-ace4-4fb2-bcd1-be1ae4979866",
              "notifications": "https://events.vin.li/api/v1/events/49f0f996-ace4-4fb2-bcd1-be1ae4979866/notifications"
            }
          },
          {
            "id": "6bcad159-a0dc-4962-97bb-52195b02abd7",
            "timestamp": "2016-12-14T22:40:28.064Z",
            "deviceId": "eb4f66ec-4050-4052-9559-baf5d8eb8511",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "dtc-on",
            "object": {
              "id": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
              "type": "vehicle"
            },
            "meta": {
              "code": "313bc7d7-1fc6-491f-9e02-c3d02e64994c"
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/6bcad159-a0dc-4962-97bb-52195b02abd7",
              "notifications": "https://events.vin.li/api/v1/events/6bcad159-a0dc-4962-97bb-52195b02abd7/notifications"
            }
          },
          {
            "id": "3aacec4e-e478-31ec-7008-0aad4093c328",
            "timestamp": "2016-12-20T17:42:33.131Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "rule-enter",
            "object": {
              "id": "b40439e2-8c9b-4684-a2c9-daaa76d9a13c",
              "type": "rule"
            },
            "meta": {
              "direction": "enter",
              "firstEval": false,
              "rule": {
                "id": "b40439e2-8c9b-4684-a2c9-daaa76d9a13c",
                "name": "got to work",
                "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                "object": {
                  "id": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                  "type": "device"
                },
                "boundaries": [
                  {
                    "id": "652c3b9c-aace-420d-aa29-0aa518659317",
                    "type": "polygon",
                    "coordinates": [
                      [
                        [
                          -96.7904305458069,
                          32.7828150725714
                        ],
                        [
                          -96.7917609214783,
                          32.782544470838
                        ],
                        [
                          -96.7914605140686,
                          32.7811914498245
                        ],
                        [
                          -96.7906773090363,
                          32.7810381061449
                        ],
                        [
                          -96.7893040180206,
                          32.7816604994394
                        ],
                        [
                          -96.788467168808,
                          32.782535450766
                        ],
                        [
                          -96.7894649505615,
                          32.7828511527404
                        ],
                        [
                          -96.7903876304626,
                          32.7828150725714
                        ],
                        [
                          -96.7904305458069,
                          32.7828150725714
                        ]
                      ]
                    ]
                  }
                ],
                "evaluated": true,
                "covered": true,
                "createdAt": "2016-12-20T01:15:38.843987+00:00",
                "links": {
                  "self": "https://rules.vin.li/api/v1/rules/b40439e2-8c9b-4684-a2c9-daaa76d9a13c",
                  "events": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events?type=rule-*&objectId=b40439e2-8c9b-4684-a2c9-daaa76d9a13c",
                  "subscriptions": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/subscriptions?objectType=rule&objectId=b40439e2-8c9b-4684-a2c9-daaa76d9a13c"
                }
              },
              "message": {
                "id": "edfe24c4-bcd0-4912-b63f-e1581eacf431",
                "timestamp": "2016-12-20T17:42:33.131Z",
                "snapshot": {
                  "location": {
                    "lat": 32.782804,
                    "lon": -96.789367
                  },
                  "accel": {
                    "maxZ": -5.094887,
                    "maxX": 0.651226,
                    "maxY": -5.899343,
                    "minX": 0.268152,
                    "minY": -6.014265,
                    "minZ": -6.703799
                  },
                  "rpm": 1280,
                  "calculatedLoadValue": 17.254901960784313,
                  "designOBDRequirements": "OBD-II as defined by the CARB",
                  "vehicleSpeed": 50,
                  "intakeManifoldPressure": 23,
                  "massAirFlow": 3.9
                }
              }
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/3aacec4e-e478-31ec-7008-0aad4093c328",
              "notifications": "https://events.vin.li/api/v1/events/3aacec4e-e478-31ec-7008-0aad4093c328/notifications"
            }
          },
          {
            "id": "217d0534-bc62-3fc3-9f58-3114fe9bc765",
            "timestamp": "2016-12-20T21:33:05.285Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": null,
            "eventType": "rule-enter",
            "object": {
              "id": "3a18675d-b404-8918-a3d4-15693472ae13",
              "type": "rule"
            },
            "meta": {
              "direction": "enter",
              "firstEval": false,
              "rule": {
                "id": "3a18675d-b404-8918-a3d4-15693472ae13",
                "name": "Speedster!",
                "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                "object": {
                  "id": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                  "type": "device"
                },
                "boundaries": [
                  {
                    "id": "95c9ea11-17ae-3991-8b2f-d3acb86672f3",
                    "type": "parametric",
                    "parameter": "vehicleSpeed",
                    "min": 65
                  }
                ],
                "evaluated": true,
                "covered": true,
                "createdAt": "2016-12-20T21:31:15.359984+00:00",
                "links": {
                  "self": "https://rules.vin.li/api/v1/rules/3a18675d-b404-8918-a3d4-15693472ae13",
                  "events": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events?type=rule-*&objectId=3a18675d-b404-8918-a3d4-15693472ae13",
                  "subscriptions": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/subscriptions?objectType=rule&objectId=3a18675d-b404-8918-a3d4-15693472ae13"
                }
              },
              "message": {
                "id": "7a8582b0-d6b4-48a9-9c34-7af932295b4a",
                "timestamp": "2016-12-20T21:33:05.285Z",
                "snapshot": {
                  "location": {
                    "lat": 32.77653,
                    "lon": -96.799442
                  },
                  "accel": {
                    "maxZ": 9.883315,
                    "maxX": 2.489982,
                    "maxY": -4.252124,
                    "minX": -0.995993,
                    "minY": -7.929636,
                    "minZ": 4.290431
                  },
                  "calculatedLoadValue": 18.431372549019606,
                  "intakeManifoldPressure": 27,
                  "rpm": 3320,
                  "massAirFlow": 6.64,
                  "longTermFuelTrimBank1": -1.5625,
                  "vehicleSpeed": 67,
                  "shortTermFuelTrimBank2": 0
                }
              }
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/217d0534-bc62-3fc3-9f58-3114fe9bc765",
              "notifications": "https://events.vin.li/api/v1/events/217d0534-bc62-3fc3-9f58-3114fe9bc765/notifications"
            }
          },
          {
            "id": "b066c41a-c243-4a40-af09-8900c0b25e7f",
            "timestamp": "2016-11-27T16:52:57.152Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "38ef2962-7fd2-4319-8389-f9a6b85a7e3f",
            "eventType": "rule-leave",
            "object": {
              "id": "6ad6dcab-4e15-334a-ba3f-5bb9a7ddb7fe",
              "type": "rule"
            },
            "meta": {
              "direction": "leave",
              "firstEval": false,
              "rule": {
                "id": "6ad6dcab-4e15-334a-ba3f-5bb9a7ddb7fe",
                "name": "radius geofence",
                "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                "object": {
                  "id": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
                  "type": "device"
                },
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
                "covered": true,
                "createdAt": "2016-07-23T05:41:28.179+00:00",
                "links": {
                  "self": "https://rules.vin.li/api/v1/rules/6ad6dcab-4e15-334a-ba3f-5bb9a7ddb7fe",
                  "events": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events?type=rule-*&objectId=6ad6dcab-4e15-334a-ba3f-5bb9a7ddb7fe",
                  "subscriptions": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/subscriptions?objectType=rule&objectId=6ad6dcab-4e15-334a-ba3f-5bb9a7ddb7fe"
                }
              },
              "message": {
                "id": "31104e29-84ec-4775-9a32-d667e6287292",
                "timestamp": "2016-11-27T16:52:57.152Z",
                "snapshot": {
                  "location": {
                    "lat": 32.823664,
                    "lon": -96.793123
                  },
                  "accel": {
                    "maxZ": -5.975958,
                    "maxX": 0.612919,
                    "maxY": -7.201795,
                    "minX": -0.727841,
                    "minY": -7.240103,
                    "minZ": -8.312711
                  },
                  "rpm": 1406,
                  "intakeManifoldPressure": 37,
                  "calculatedLoadValue": 33.333333333333336,
                  "massAirFlow": 9.76,
                  "vehicleSpeed": 34
                }
              }
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/b066c41a-c243-4a40-af09-8900c0b25e7f",
              "notifications": "https://events.vin.li/api/v1/events/b066c41a-c243-4a40-af09-8900c0b25e7f/notifications"
            }
          },
          {
            "id": "747e3642-b481-4589-a7af-cbb512319d03",
            "timestamp": "2016-12-20T17:35:43.357Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "trip-started",
            "object": {
              "id": "1b8b9447-428c-4c0d-631d-1bc27b401c15",
              "type": "trip"
            },
            "meta": {
              "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f"
            },
            "links": {
              "self": "https://events.vin.li/api/v1/events/747e3642-b481-4589-a7af-cbb512319d03",
              "notifications": "https://events.vin.li/api/v1/events/747e3642-b481-4589-a7af-cbb512319d03/notifications"
            }
          },
          {
            "id": "97baaf93-d7ac-443b-a296-4e6cbb1a1cc7",
            "timestamp": "2016-12-20T17:35:43.357Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "startup",
            "object": {
              "id": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
              "type": "vehicle"
            },
            "meta": null,
            "links": {
              "self": "https://events.vin.li/api/v1/events/97baaf93-d7ac-443b-a296-4e6cbb1a1cc7",
              "notifications": "https://events.vin.li/api/v1/events/98bbaf93-d7bc-444b-b296-4e6cbb1a1cc8/notifications"
            }
          },
          {
            "id": "b3d2444-78ec-45d8-8073-13421ad2ef96",
            "timestamp": "2016-12-19T13:31:00.491Z",
            "deviceId": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "vehicleId": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
            "eventType": "phone-home",
            "object": {
              "id": "48ef1264-7fd2-4319-8789-g9a6b85b7a8f",
              "type": "vehicle"
            },
            "meta": null,
            "links": {
              "self": "https://events.vin.li/api/v1/events/b3d2444-78ec-45d8-8073-13421ad2ef96",
              "notifications": "https://events.vin.li/api/v1/events/b3d2444-78ec-45d8-8073-13421ad2ef96/notifications"
            }
          },
        ],
        "meta": {
          "pagination": {
            "remaining": 7993,
            "until": "2016-12-20T21:04:26.443Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 10,
            "sortDir": "desc",
            "links": {
              "prior": "https://events.vin.li/api/v1/devices/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events?limit=100&until=1482013267165"
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
