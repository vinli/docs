Notifications
--------------

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
              "remaining": 2,
              "until": "2016-09-15T18:38:44.036Z",
              "since": "1970-01-01T00:00:00.000Z",
              "limit": 20,
              "sortDir": "desc",
              "links": {
                "prior": "https://events.vin.li/api/v1/subscriptions/f4366076-afe0-4b05-83ff-55b6ddde0984/notifications?until=1473961364647"
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
              "remaining": 0,
              "until": "2016-09-15T20:19:32.978Z",
              "since": "1970-01-01T00:00:00.000Z",
              "limit": 20,
              "sortDir": "desc",
              "links": {}
              }
            }
          }
