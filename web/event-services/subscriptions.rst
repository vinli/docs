Subscriptions
-------------

In order to receive notification for vehicle events, your application must subscribe to events for each device individually.

Each Subscription relates to a given event or class of events from a given Device and specifies the external URL that will be called when the event occurs and any additional "App Data" that should be included.


Notification Payloads
````````````````````````

When a subscription is triggered, an HTTP call using the "POST" method is made to the Subscription's URL.  This call uses content-type of "application/json" and sends a JSON representation containing a `notification` root object along with representations of the Event that triggered the notification and the associated Subscription. Below are several examples of Notifications for different types of Events.

Rule-Leave
==========

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


Collision
=========

.. code-block:: json

      {
        "notification": {
          "event": {
            "id": "edae9b7a-c447-442d-aead-ee0bf4f5e6b4",
            "timestamp": "2016-08-22T23:12:59.607Z",
            "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
            "stored": "2016-08-22T23:13:15.167Z",
            "storageLatency": 15560,
            "eventType": "collision",
            "object": {
              "id": "ba8d8890-3d4d-413a-ad8e-a3269d990e91",
              "type": "vehicle"
            },
            "links": {
              "self": "http://10.200.37.245:30003/api/v1/events/edae9b7a-c447-442d-aead-ee0bf4f5e6b4",
              "notifications": "http://10.200.37.245:30003/api/v1/events/edae9b7a-c447-442d-aead-ee0bf4f5e6b4/notifications"
            }
          },
          "subscription": {
            "id": "f4366076-afe0-4b05-83ff-55b6ddde0984",
            "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
            "eventType": "collision",
            "url": "https://myapp.com/notifications",
            "appData": null,
            "createdAt": "2016-08-22T23:11:36.814Z",
            "updatedAt": "2016-08-22T23:11:36.814Z",
            "links": {
              "self": "http://10.200.37.245:30003/api/v1/subscriptions/f4366076-afe0-4b05-83ff-55b6ddde0984",
              "notifications": "http://10.200.37.245:30003/api/v1/subscriptions/f4366076-afe0-4b05-83ff-55b6ddde0984/notifications"
            }
          }
        }
      }


DTC-On
======

.. code-block:: json

        {
          "notification": {
            "event": {
              "id": "aa2842c3-b647-48a1-80f1-cc6019ce387c",
              "timestamp": "2016-08-22T23:12:20.003Z",
              "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
              "stored": "2016-08-22T23:12:22.036Z",
              "storageLatency": 2033,
              "eventType": "dtc-on",
              "meta": {
                "code": "313cc7d7-1ac6-491c-9e02-a3d08e62984a"
              },
              "object": {
                "id": "ba8d8890-3d4d-413a-ad8e-a3269d990e91",
                "type": "vehicle"
              },
              "links": {
                "self": "http://10.220.0.66:30003/api/v1/events/aa2842c3-b647-48a1-80f1-cc6019ce387c",
                "notifications": "http://10.220.0.66:30003/api/v1/events/aa2842c3-b647-48a1-80f1-cc6019ce387c/notifications"
              }
            },
            "subscription": {
              "id": "e480343c-172a-41da-81ef-ce7950790ee0",
              "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
              "eventType": "dtc-on",
              "url": "https://myapp.com/notifications",
              "appData": null,
              "createdAt": "2016-08-22T23:09:22.023Z",
              "updatedAt": "2016-08-22T23:09:22.023Z",
              "links": {
                "self": "http://10.220.0.66:30003/api/v1/subscriptions/e480343c-172a-41da-81ef-ce7950790ee0",
                "notifications": "http://10.220.0.66:30003/api/v1/subscriptions/e480343c-172a-41da-81ef-ce7950790ee0/notifications"
              }
            }
          }
        }

Distance-Trigger
================

.. code-block:: json

      {
        "notification": {
          "event": {
            "id": "4449b8a1-88ce-479e-83ba-46d233895519",
            "timestamp": "2016-07-18T22:32:41.737Z",
            "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
            "stored": "2016-07-18T22:32:41.860Z",
            "storageLatency": 123,
            "eventType": "distance-trigger",
            "meta": {
              "odometerTrigger": {
                "id": "bc043c26-3d79-44ce-b08e-8193f4c5e493",
                "vehicleId": "03d8ec74-523b-4ff7-8f6f-8228146b93b9",
                "type": "specific",
                "threshold": 24146537.36,
                "events": 0,
                "links": {
                  "vehicle": "https://platform.vin.li/api/v1/vehicles/03d8ec74-523b-4ff7-8f6f-8228146b93b9"
                }
              },
              "estimatedOdometer": 24158103.340000004
            },
            "object": {
              "id": "bc043c26-3d79-44ce-b08e-8193f4c5e493",
              "type": "odometer-trigger"
            },
            "links": {
              "self": "http://10.200.37.245:30003/api/v1/events/4449b8a1-88ce-479e-83ba-46d233895519",
              "notifications": "http://10.200.37.245:30003/api/v1/events/4449b8a1-88ce-479e-83ba-46d233895519/notifications"
            }
          },
          "subscription": {
            "id": "2fc61637-8e2d-465f-8518-cce48f205faf",
            "deviceId": "eb4f66ec-4050-4052-9559-baf5d8eb8511",
            "eventType": "distance-trigger",
            "url": "https://myapp.com/notifications",
            "appData": null,
            "createdAt": "2016-07-18T22:09:34.704Z",
            "updatedAt": "2016-07-18T22:09:34.704Z",
            "links": {
              "self": "http://10.200.37.245:30003/api/v1/subscriptions/2fc61637-8e2d-465f-8518-cce48f205faf",
              "notifications": "http://10.200.37.245:30003/api/v1/subscriptions/2fc61637-8e2d-465f-8518-cce48f205faf/notifications"
            }
          }
        }
      }

Startup
=======

.. code-block:: json

      {
        "notification": {
          "event": {
            "id": "5eca3320-7037-4eaf-8cea-08328bf25408",
            "timestamp": "2016-08-24T20:26:04.816Z",
            "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
            "stored": "2016-08-24T20:26:08.809Z",
            "storageLatency": 3993,
            "eventType": "startup",
            "object": {
              "id": "2271db32-aa6c-4ae5-9d68-f371eb3d1cfb",
              "type": "vehicle"
            },
            "links": {
              "self": "http://10.220.0.66:30003/api/v1/events/5eca3320-7037-4eaf-8cea-08328bf25408",
              "notifications": "http://10.220.0.66:30003/api/v1/events/5eca3320-7037-4eaf-8cea-08328bf25408/notifications"
            }
          },
          "subscription": {
            "id": "050ea013-33f2-49ae-bcf2-f23032e6ca30",
            "deviceId": "4bffefbb-9fba-43ee-aebe-ed7f7f2fae84",
            "eventType": "startup",
            "url": "https://myapp.io/startup",
            "object": {
              "id": "2271db32-aa6c-4ae5-9d68-f371eb3d1cfb",
              "type": "vehicle"
            },
            "appData": null,
            "createdAt": "2016-08-24T20:25:18.017Z",
            "updatedAt": "2016-08-24T20:25:18.017Z",
            "links": {
              "self": "http://10.220.0.66:30003/api/v1/subscriptions/050ea013-33f2-49ae-bcf2-f23032e6ca30",
              "notifications": "http://10.220.0.66:30003/api/v1/subscriptions/050ea013-33f2-49ae-bcf2-f23032e6ca30/notifications"
            }
          }
        }
      }


Note that the `appData` attribute of the `subscription` property contains the Application-specific data that you created the Subscription with, if applicable.

In the example above, the Subscription triggered is associated with a Rule.  In this case, additional information is made available in the Notification including a representation of the Rule in the `meta` property.  Additionally, a very useful property `firstEval` is provided that lets your Application know whether or not this is the first evaluation of the Rule.  The first evaluation of a Rule in which it can be established that the device is covered or not covered by the boundaries will always result in a notification.  Using the `firstEval` property, your App can determine if the device was previously in a different state or was just in an unknown state.


Create a Subscription
```````````````````````

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
````````````````````````````````````

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
`````````````````````````````

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
```````````````````````

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
``````````````````````

Request
+++++++

.. code-block:: json

      DELETE https://events.vin.li/api/v1/subscriptions/917fb546-5666-4fdd-aed6-53fa099b313b
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT
