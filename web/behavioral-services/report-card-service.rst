Report Card Service
~~~~~~~~~~~~~~~~~~~


The Driver Report Card contains the overall score for that scope.

Each score is represented by a `major` and `minor` score.  These are split in order to allow for easy rendering to the end-user, but are meant to be concatenated to produce school-like grades such as "A-" or "C+".


Weekly Report Card for a Device
```````````````````````````````

Returns a Report Card based on historical data for a specified week of the year.  The week is denoted using the ISO 8601 date format.  For example, "2014-W16" represents the 16th week of 2014.

In some cases, not enough information was gathered during the course of a week to generate a Report Card.  In these cases, the grades will be reported as "I" (for "Incomplete" to keep the school report card metaphore going).

Request
+++++++

.. code-block:: json

      GET https://behavior.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/report_card?week=2014-W16
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "report_card" : {
          "id": "549d628c-48dc-412d-8087-44a9f82f187e",
          "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "vehicleId": "ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55",
          "tripId": "b9e58eb4-0743-45e9-b9c6-86500f5412bb",
          "grade": "I",
          "links": {
            "self": "https://behavioral-dev.vin.li/api/v1/report_cards/549d628c-48dc-412d-8087-44a9f82f187e",
            "trip": "https://trips-dev.vin.li/api/v1/trips/b9e58eb4-0743-45e9-b9c6-86500f5412bb",
            "device": "https://platform-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55"
          }
        }
      }


Lifetime Report Card for a Device
`````````````````````````````````

Returns a Report Card based on all historical data available for a given Device.

Request
+++++++

.. code-block:: json

      GET https://behavior.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/report_card
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "report_card" : {
          "id": "549d628c-48dc-412d-8087-44a9f82f187e",
          "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "vehicleId": "ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55",
          "tripId": "b9e58eb4-0743-45e9-b9c6-86500f5412bb",
          "grade": "I",
          "links": {
            "self": "https://behavioral-dev.vin.li/api/v1/report_cards/549d628c-48dc-412d-8087-44a9f82f187e",
            "trip": "https://trips-dev.vin.li/api/v1/trips/b9e58eb4-0743-45e9-b9c6-86500f5412bb",
            "device": "https://platform-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55"
          }
        }
      }


Report Card for a Trip
``````````````````````

The Trip-specific Report Card contains the same data as the Long-Term and Lifetime Report Card but is specific for a particular Trip.

In some cases, the Trip is too short to generate the data necessary for the Report Card analysis to be run.  In these cases, the grades will be reported as "I".

Request
+++++++

.. code-block:: json

      GET https://behavior.vin.li/api/v1/trips/1f6ed1a0-6044-4505-a828-715c0f3eccf7/report_card
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "report_card" : {
          "id": "549d628c-48dc-412d-8087-44a9f82f187e",
          "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
          "vehicleId": "ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55",
          "tripId": "b9e58eb4-0743-45e9-b9c6-86500f5412bb",
          "grade": "I",
          "links": {
            "self": "https://behavioral-dev.vin.li/api/v1/report_cards/549d628c-48dc-412d-8087-44a9f82f187e",
            "trip": "https://trips-dev.vin.li/api/v1/trips/b9e58eb4-0743-45e9-b9c6-86500f5412bb",
            "device": "https://platform-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6b58",
            "vehicle": "https://platform-dev.vin.li/api/v1/vehicles/ca10cd7a-d2a5-4bb3-b47b-2aa0b8848f55"
          }
        }
      }

