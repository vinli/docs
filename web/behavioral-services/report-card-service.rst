Report Card Service
~~~~~~~~~~~~~~~~~~~


The Driver Report Card contains categorized scores for each of three categories as well as information as to which specific factors added to or detracted from the category's score.

Each score is represented by a `major` and `minor` score.  These are split in order to allow for easy rendering to the end-user, but are meant to be concatenated to produce school-like grades such as "A-" or "C+".


Weekly Report Card for a Device
```````````````````````````````

Returns a Report Card based on historical data for a specified week of the year.  The week is denoted using the ISO 8601 date format.  For example, "2014-W16" represents the 16th week of 2014 (_________).

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
          "deviceId" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "overallGrade" : {
            "major" : "B",
            "minor" : "-",
          },
          "driverBehavior" : {
            "major" : "C",
            "minor" : "+",
            "factors" : {
              "good" : [ "acceleration", "turns" ],
              "bad" : [ "braking" ]
          },
          "vehicleCondition" : {
            "major" : "A",
            "minor" : "",
            "factors" : {
              "good" : [ "brakesAndTires", "engineEfficiency" ],
              "bad" : []
          },
          "travelPattern" : {
            "major" : "D",
            "minor" : "+"
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
          "deviceId" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "overallGrade" : {
            "major" : "B",
            "minor" : "-",
          },
          "driverBehavior" : {
            "major" : "C",
            "minor" : "+",
            "factors" : {
              "good" : [ "acceleration", "turns" ],
              "bad" : [ "braking" ]
          },
          "vehicleCondition" : {
            "major" : "A",
            "minor" : "",
            "factors" : {
              "good" : [ "brakesAndTires", "engineEfficiency" ],
              "bad" : []
          },
          "travelPattern" : {
            "major" : "D",
            "minor" : "+"
          }
        }
      }


Report Card for a Trip
``````````````````````

The Trip-specific Report Card contains the same data as the Long-Term and Lifetime Report Card but is specific for a particular Trip.

In some cases, the Trip is too short to generate the data necessary for the Report Card analysis to be run.  In these cases, the grades will be reported as "I".

Note that the `travelPattern` score reported for a given Trip is actually based on a rolling window of Trips as a multiple Trips are required in order to determine this score.

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
          "deviceId" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "tripId" : "1f6ed1a0-6044-4505-a828-715c0f3eccf7",
          "overallGrade" : {
            "major" : "A",
            "minor" : "-",
          },
          "driverBehavior" : {
            "major" : "C",
            "minor" : "-",
            "factors" : {
              "good" : [ "acceleration"],
              "bad" : [ "braking", "speed" ]
          },
          "vehicleCondition" : {
            "major" : "B",
            "minor" : "",
            "factors" : {
              "good" : [ "brakesAndTires" ],
              "bad" : []
          },
          "travelPattern" : {
            "major" : "D",
            "minor" : "+"
          }
        }
      }

