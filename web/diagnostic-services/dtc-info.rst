DTC Info Service
~~~~~~~~~~~~~~~~

Get Information About a DTC Code
````````````````````````````````

There's a lot of information encoded in the DTC codes reported by a Vehicle.  This method is meant to provide this information for a given DTC code so that your Application can present useful information to the end-user.

Request
+++++++

.. code-block:: json

      GET https://diagnostics.vin.li/api/v1/codes?number=P0171
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "code" : {
          make: 'generic',
          twoByte: {
            number: 'P0001',
            description: 'Fuel Volume Regulator Control Circuit/Open'
          },
          threeByte: {
            number: 'P0001',
            ftb: '13',
            fault: 'Circuit Open',
            description: 'Fuel Volume Regulator Control'
          }
        }
      }
