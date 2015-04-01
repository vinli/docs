Event Service
~~~~~~~~~~~~~

### Get Events for a Rule

Returns the list all events for a given rule reverse-chronological order.  Each Event contains information regarding the device, the message that triggered the event, and the state of the notification.

Notification state is useful in debugging notification handlers on your Application.  This state property (as well as the `response` property) will inform you as to the result of Event Services' attempt to call the notification URL.


Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events
      Accept: application/json

Parameters
++++++++++

* `deviceId` - (optional) filter events for those for a given device


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "events" : [
          {
            "id" : "2bd8d090-d7ec-11e3-9c1a-0800200c9a66",
            "deviceId" : "51808e00-d7ec-11e3-9c1a-0800200c9a66",
            "messageId" : "76149d0f-8746-4ca4-a3d8-cb4a84131659",
            "timestamp" : "2014-07-18T01:17:23.723Z",
            "notificationUrl" : "https://www.myapp.com/vinli_events?internalRuleId=1314",
            "notificationMetadata" : {
              "userFirstName": "John",
              "userLastName": "Sample",
              "smsPhoneNumber": "2145551212"
            },
            "state" : "pending_notification"
          },
          {
            "id" : "d8df9452-d7ec-11e3-9c1a-0800200c9a66",
            "deviceId" : "51808e00-d7ec-11e3-9c1a-0800200c9a66",
            "messageId" : "ca715565-0160-4ff3-bfde-370e526d3817",
            "timestamp" : "2014-07-18T09:32:33.618Z",
            "notificationUrl" : "https://www.myapp.com/vinli_events?internalRuleId=1314",
            "notificationMetadata" : {
              "userFirstName": "John",
              "userLastName": "Sample",
              "smsPhoneNumber": "2145551212"
            },
            "state" : "notification_error",
            "response" : {
              "statusCode" : "500",
              "body" : "Internal Error Occurred"
            }
          },
          {
            "id" : "3e482dae-d7ec-11e3-9c1a-0800200c9a66",
            "deviceId" : "f459930c-85d4-4d82-b4c0-0a0249c3d55f",
            "messageId" : "4f308749-d02e-45a7-b473-ff29f2157404",
            "timestamp" : "2014-07-18T12:20:53.971Z",
            "notificationUrl" : "https://www.myapp.com/vinli_events?internalRuleId=1314",
            "notificationMetadata" : {
              "userFirstName": "John",
              "userLastName": "Sample",
              "smsPhoneNumber": "2145551212"
            },
            "state" : "successful",
            "response" : {
              "statusCode" : "201",
              "body" : "Notification Registered"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "remaining" : 281,
            "until" : 13996891904523,
            "limit" : 20,
            "links" : {
              "latest" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events&limit=20",
              "prior" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events?until=13996891010225&limit=20"
            }
          }
        }
      }
