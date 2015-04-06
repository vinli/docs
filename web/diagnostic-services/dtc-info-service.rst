DTC Info Service
~~~~~~~~~~~~~~~~

Get Information About a DTC Code
````````````````````````````````

There's a lot of information encoded in the DTC codes reported by a Vehicle.  This method is meant to provide this information for a given DTC code so that your Application can present useful information to the end-user.

Request
+++++++

.. code-block:: json

      GET https://diagnostics.vin.li/api/v1/dtc_codes/P0171
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "dtc_code" : {
          "id" : "P0171",
          "name" : "System Too Lean (Bank 1)",
          "system" : "powertrain",
          "codeType" : "generic",
          "subSystem" : "emission_management",
          "shortDescription" : "O2 Sensor (Bank 1) has detected a lean exhaust condition",
          "longDescription" : "...",
          "possibleSymptoms" : [
            "Lack of Power",
            "Engine Knock",
            "Rough at Idle"
          ],
          "possibleCauses" : [
            "Faulty O2 Sensor (Bank 1)",
            "Vacuum leak downstream of the MAF sensor",
            "Cracked vacuum or PCV line/connection",
            "Exhaust leak between engine and first oxygen sensor",
            ...
          ],
          "possibleResolutions" : [
            "Replace O2 Sensor (Bank 1)",
            ...
          ],a
          "severity" : "low"
        }
      }
