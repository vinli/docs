DTC Notification Service
~~~~~~~~~~~~~~~~~~~~~~~~

When a Device detects a new DTC code within the Vehicle it is attached to, it sends a message to the Vinli Platform informing it as such.  Your Application can subscribe to receive notifications when these events occur using the DTC Notification Service.

Create a new DTC Notification
`````````````````````````````

Request
+++++++

.. code-block:: json

      POST https://diagnostics.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/dtc_notifications
      Accept: application/json
      Content-Type: application/json

      {
        "dtcNotification" : {
          "notificationUrl" : "https://www.myapp.com/vinli_dtc_events?internalDeviceId=1314",
          "notificationMetadata" : {
            "userFirstName": "John",
            "userLastName": "Sample",
            "smsPhoneNumber": "2145551212"
          }
        }
      }

Response
++++++++

.. code-block:: json

      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://diagnostics.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/dtc_notifications/e1fc2404-388a-49f7-8435-8c926977174a

      {
        "dtcNotification" : {
          "id": "e1fc2404-388a-49f7-8435-8c926977174a",
          "deviceId" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "notificationUrl" : "https://www.myapp.com/vinli_dtc_events?internalDeviceId=1314",
          "notificationMetadata" : {
            "userFirstName": "John",
            "userLastName": "Sample",
            "smsPhoneNumber": "2145551212"
          }
        }
      }