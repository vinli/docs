Rule Service
~~~~~~~~~~~~

The Rule Service allows your application to manage the rules for devices associated with it.

It's important to note that Rules are immutable.  Once they are created, they cannot be modified; they can only be deleted and another rule created.  This is designed this way such that the continuity of the Rule and the Vehicles whose state is maintained for this rule remains consistent.  The Vehicle is allowed to move in space, but the Rule is not.


List all Rules
``````````````

Returns a paginated list of all rules for your Application.

Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/rules
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "rules" : [
          {
            "id" : "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "name" : "Speed over 70mph",
            "device" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
            "boundaries" : [
              {
                "type" : "parametric",
                "parameter" : "vehicleSpeed",
                "min" : 70
              }
            ],
            "links" : {
              "self" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66",
              "events" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events"
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
              "first" : "https://events.vin.li/api/v1/rules?offset=0&limit=20",
              "last" : "https://events.vin.li/api/v1/rules?offset=1420&limit=20",
              "next" : "https://events.vin.li/api/v1/rules?offset=20&limit=20"
            }
          }
        }
      }


List all Rules for a Device
```````````````````````````

Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/rules
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "rules" : [
        {
          "id" : "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
          "name" : "Speed over 70mph",
          "device" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "boundaries" : [
            {
              "type" : "parametric",
              "parameter" : "vehicleSpeed",
              "min" : 70
            }
          ],
          "links" : {
            "self" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "events" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events"
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
              "first" : "https://events.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/rules?offset=0&limit=20",
              "last" : "https://events.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/rules?offset=1420&limit=20",
              "next" : "https://events.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/rules?offset=20&limit=20"
            }
          }
        }
      }


Get a Specific Rule
```````````````````

Request
+++++++

.. code-block:: json

      GET https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "rule" : {
          "id" : "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
          "name" : "Speed over 35mph near Superdome",
          "boundaries" : [
            {
              "type" : "parametric",
              "parameter" : "vehicleSpeed",
              "min" : 35
            },
            {
              "type" : "radius",
              "lon" : -90.0811,
              "lat" : 29.9508,
              "radius" : 500
            }
          ],
          "device" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "notificationUrl" : "https://www.myapp.com/vinli_events?internalRuleId=1314",
          "notificationMetadata" : {
            "userFirstName": "John",
            "userLastName": "Sample",
            "smsPhoneNumber": "2145551212"
          },
          "links" : {
            "self" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "events" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events"
          }
        }
      }


Create a Rule for a Device
``````````````````````````

Request
+++++++

.. code-block:: json

      POST https://events.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/rules
      Accept: application/json
      Content-Type: application/json

      {
        "rule" : {
          "name" : "Speed over 35mph near Superdome",
          "boundaries" : [
            {
              "type" : "parametric",
              "parameter" : "vehicleSpeed",
              "min" : 35,
              "max" : null
            },
            {
              "type" : "radius",
              "lon" : -90.0811,
              "lat" : 29.9508,
              "radius" : 500
            }
          ],
          "notificationUrl" : "https://www.myapp.com/vinli_events?internalRuleId=1314",
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
      Location: https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66

      {
        "rule" : {
          "id" : "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
          "name" : "Speed over 35mph near the Superdome",
          "boundaries" : [
            {
              "type" : "parametric",
              "parameter" : "vehicleSpeed",
              "min" : 35
            },
            {
              "type" : "radius",
              "lon" : -90.0811,
              "lat" : 29.9508,
              "radius" : 500
            }
          ],
          "device" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "notificationUrl" : "https://www.myapp.com/vinli_events?internalRuleId=1314",
          "notificationMetadata" : {
            "userFirstName": "John",
            "userLastName": "Sample",
            "smsPhoneNumber": "2145551212"
          },
          "links" : {
            "self" : "https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66"
            "events" : "/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/events"
          }
        }
      }


Delete a Rule
`````````````

Request
+++++++

.. code-block:: json

      DELETE https://events.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66

Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT

