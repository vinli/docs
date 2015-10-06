Rule API
========

The Rule Service allows your application to manage the rules for devices.

Rules are immutable.  Once created, a rule cannot be modified. To change a Rule, your app must delete an existing rule, and then create another one. Immutability ensures that a Rule is always in a perfectly consistent state.


List all Rules for a Device
```````````````````````````

Request
+++++++

.. code-block:: json

      GET https://rules.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/rules
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
            "deviceId" : "de01abb1-453d-4293-831a-f0d804b48fdf",
            "evaluated": true,
            "covered": false,
            "createdAt": "2015-06-01T21:26:51.086Z",
            "links" : {
              "self" : "https://rules.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66",
              "events": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/events?type=rule&objectId=68d489c0-d7a2-11e3-9c1a-0800200c9a66",
              "subscriptions": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions?objectType=rule&objectId=68d489c0-d7a2-11e3-9c1a-0800200c9a66"
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
              "first" : "https://rules.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/rules?offset=0&limit=20",
              "last" : "https://rules.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/rules?offset=1420&limit=20",
              "next" : "https://rules.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/rules?offset=20&limit=20"
            }
          }
        }
      }


Get a Specific Rule
```````````````````

Request
+++++++

.. code-block:: json

      GET https://rules.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66
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
          "deviceId" : "de01abb1-453d-4293-831a-f0d804b48fdf",
          "links" : {
            "self" : "https://rules.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "events": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/events?type=rule&objectId=68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "subscriptions": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions?objectType=rule&objectId=68d489c0-d7a2-11e3-9c1a-0800200c9a66"
          }
        }
      }


Create a Rule for a Device
``````````````````````````

Request
+++++++

.. code-block:: json

      POST https://rules.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/rules
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
          ]
        }
      }


Response
++++++++

.. code-block:: json

      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://rules.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66

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
          "deviceId" : "de01abb1-453d-4293-831a-f0d804b48fdf",
          "links" : {
            "self" : "https://rules.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "events": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/events?type=rule&objectId=68d489c0-d7a2-11e3-9c1a-0800200c9a66",
            "subscriptions": "https://events.vin.li/api/v1/devices/de01abb1-453d-4293-831a-f0d804b48fdf/subscriptions?objectType=rule&objectId=68d489c0-d7a2-11e3-9c1a-0800200c9a66"
          }
        }
      }


Delete a Rule
`````````````

Request
+++++++

.. code-block:: json

      DELETE https://rules.vin.li/api/v1/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66

Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT


.. toctree::
   :maxdepth: 1

   rule-services