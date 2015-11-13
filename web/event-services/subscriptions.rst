Subscriptions
-------------

In order to receive notification for vehicle events, your application must subscribe to events for each device individually.

Each Subscription relates to a given event or class of events from a given Device and specifies the external URL that will be called when the event occurs and any additional "App Data" that should be included.


Notification Payload
````````````````````````

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