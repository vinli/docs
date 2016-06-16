Virtual Vinli Dummy Service
---------------------------

Create a Dummy Device
`````````````````````

Request
+++++++

.. code-block:: json

  POST https://dummies.vin.li/api/v1/dummies
  Content-Type: application/json

  {
     "dummy":{
        "name":"YourDummyName"
     }
  }

Response
++++++++
.. code-block:: json

  {
    "dummy": {
      "id": "f57d3b8f-6e2d-4038-a54a-bfbd9b52bcf3",
      "name": "YourDummyName",
      "deviceId": "5067097d-d9b0-49d7-ac06-badd1030670e",
      "caseId": "VV4G86Z",
      "links": {
        "self": "https://dummies.vin.li/api/v1/dummies/f57d3b8f-6e2d-4038-a54a-bfbd9b52bcf3",
        "runs": "https://dummies.vin.li/api/v1/dummies/f57d3b8f-6e2d-4038-a54a-bfbd9b52bcf3/runs",
        "device": "https://platform.vin.li/api/v1/devices/5067097d-d9b0-49d7-ac06-badd1030670e",
        "messages": "https://telemetry.vin.li/api/v1/devices/5067097d-d9b0-49d7-ac06-badd1030670e/messages",
        "events": "https://events.vin.li/api/v1/devices/5067097d-d9b0-49d7-ac06-badd1030670e/events"
      }
    }
  }


List Dummy Devices
```````````````````

Request
+++++++

.. code-block:: json

  GET https://dummies.vin.li/api/v1/dummies
  Accept: application/json

Response
++++++++
.. code-block:: json

  {
    "dummies": [
      {
        "id": "m2900t1f-7ca5-4641-j4b6-623cae742aa5",
        "name": "84_Sheepdog",
        "deviceId": "7gka0j62-858f-51b2-a5b7-br13c469158k",
        "caseId": "VV6L0FS",
        "links": {
          "self": "https://dummies.vin.li/api/v1/dummies/m2900t1f-7ca5-4641-j4b6-623cae742aa5",
          "runs": "https://dummies.vin.li/api/v1/dummies/m2900t1f-7ca5-4641-j4b6-623cae742aa5/runs",
          "device": "https://platform.vin.li/api/v1/devices/7eac0d62-854f-41c1-a5b2-ba13c460058a",
          "messages": "https://telemetry.vin.li/api/v1/devices/7eac0d62-854f-41c1-a5b2-ba13c460058a/messages",
          "events": "https://events.vin.li/api/v1/devices/7eac0d62-854f-41c1-a5b2-ba13c460058a/events"
        }
      },
      {
        "id": "4f1c5c34-2b61-4dhe-824b-2c517f69bdwf",
        "name": "VV_4_the_docs",
        "deviceId": "21f1688b-0374-41y3-9d08-g2fcaac53f31",
        "caseId": "VVA39E1",
        "links": {
          "self": "https://dummies.vin.li/api/v1/dummies/4g1c5v34-2b61-4dhe-824b-2c517f69bdwf",
          "runs": "https://dummies.vin.li/api/v1/dummies/4g1c5v34-2b61-4dhe-824b-2c517f69bdwf/runs",
          "device": "https://platform.vin.li/api/v1/devices/21f1688b-0374-41y3-9d08-g2fcaac53f31",
          "messages": "https://telemetry.vin.li/api/v1/devices/21f1688b-0374-41y3-9d08-g2fcaac53f31/messages",
          "events": "https://events.vin.li/api/v1/devices/21f1688b-0374-41y3-9d08-g2fcaac53f31/events"
        }
      }
    ],
    "meta": {
      "pagination": {
        "total": 2,
        "limit": 20,
        "offset": 0,
        "links": {
          "first": "https://dummies.vin.li/api/v1/dummies?offset=0&limit=20",
          "last": "https://dummies.vin.li/api/v1/dummies?offset=0&limit=20"
        }
      }
    }
