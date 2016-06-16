Virtual Vinli Runs
------------------

You can send your Dummy Device on a Dummy Route by creating a Run.

Create a Run
````````````

Request
+++++++

.. code-block:: json

  POST https://dummies.vin.li/api/v1/dummies/{dummy_Id}/runs
  Content-Type: application/json
  {
    "run": {
      "vin": "VVV12912912913456",
      "routeId": "8e90cf47-c6c1-486d-9ba8-194f569c7309"
    }
  }

Parameters
++++++++++

* `vin` - Required. A made up, 17 digit number that must start with 'VV'
* `routeID` - Required. A Dummy Route of your choice
* `repeat` - Optional boolean. Defaults to false. If true, will automatically restart the run after completion. If false, will not automatically restart the run.


Response
++++++++
.. code-block:: json
  {
    "run": {
      "id": "797286ff-fc37-42f8-b633-802a0a192acb",
      "status": {
        "routeId": "8e90cf47-c6c1-486d-9ba8-194f569c7309",
        "repeat": false,
        "state": "starting"
      },
      "links": {
        "self": "https://dummies.vin.li/api/v1/dummies/d2905f1f-7da5-4640-b4b6-427cae712aa3/runs/_current"
      }
    }
  }


Get Current Run
```````````````

Request
+++++++

.. code-block:: json

  GET https://dummies.vin.li/api/v1/dummies/{dummy_Id}/runs/_current
  Content-Type: application/json



Response
++++++++
.. code-block:: json
  {
    "run": {
      "id": "b92fa4f2-85e0-4e22-96cf-8daabdd0c02d",
      "status": {
        "routeId": "8e90cf47-c6c1-486d-9ba8-194f569c7309",
        "repeat": false,
        "state": "pending"
      },
      "links": {
        "self": "https://dummies.vin.li/api/v1/dummies/d2905f1f-7da5-4640-b4b6-427cae712aa3/runs/_current"
      }
    }
  }


Delete the Current Run
``````````````````````

Request
+++++++

.. code-block:: json

  DELETE https://dummies.vin.li/api/v1/dummies/{dummy_Id}/runs/_current
  Content-Type: application/json


Run may take up to 1 minute to delete.
