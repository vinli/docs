Device Service
~~~~~~~~~~~~~~

The root element in all interaction with the Vinli platform is the Device.  Each Vinil Basic device has an associated Device ID by which it is referred to within the platform.  However, before your application can access any data or perform any actions on a Device, it must be authorized by the owner of the device and then added to your application's device list (using the "Register a Device" method below).


List all Devices
````````````````

This returns a paginated list of devices that are registered with your application sorted chronologically by when the device was added.

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "devices" : [
          {
            "id" : "8b8a1810-d6d8-11e3-9c1a-0800200c9a66",
            "links" : {
              "self" : "https://platform.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66",
              "groups" : "https://platform.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/groups",
              "vehicles" : "https://platform.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/vehicles",
              "latestVehicle" : "https://platform.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest"
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
              "first" : "https://platform.vin.li/api/v1/devices?offset=0&limit=20",
              "last" : "https://platform.vin.li/api/v1/devices?offset=1420&limit=20",
              "next" : "https://platform.vin.li/api/v1/devices?offset=20&limit=20"
            }
          }
        }
      }


Register a Device
`````````````````

Your application may register a device after it has been authorized by the owner of the device (See section above on "Authentication for User Actions").  This step is necessary before your application can access any data from the device or perform any actions on the device.

A two-step process allow you to manage device authorization independent of user action.  You can remove a device without requiring a user to revoke access to the device.


Request
+++++++

.. code-block:: json

      POST https://platform.vin.li/api/v1/devices
      Content-Type: application/json
      Accept: application/json

      {
        "device" : {
          "id" : "821374c0-d6d8-11e3-9c1a-0800200c9a66"
        }
      }

Response:
++++++++

.. code-block:: json

      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66

      {
        "device" : {
          "id" : "821374c0-d6d8-11e3-9c1a-0800200c9a66",
          "links" : {
            "self" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66",
            "groups" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups",
            "vehicles" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles",
            "latestVehicle" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest"
          }
        }
      }


Get a Device
````````````

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "device" : {
          "id" : "821374c0-d6d8-11e3-9c1a-0800200c9a66",
          "links" : {
            "self" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66",
            "groups" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups",
            "vehicles" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles",
            "latestVehicle" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest"
          }
        }
      }


Deregister a Device
````````````````````````````````

Deregistering a Device from your application prevents you from accessing that device's data.  Note this has several various effects on other section of the Vinli Platform.  For instance,  Event Services will remove any Rules associated with the device, Safety Services will remove any Emergency Contact actions from the Device (if your application registered the Device with Safety Services), and Diagnostic Services will remove any DTC alerts for this Device registered by your Application.

It's important to note that deregistering a Device is an Application-level action that will have no effect on any other Application (yours or someone else's) that has been authorized for the Device.


Request
+++++++

.. code-block:: json

      DELETE https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66


Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT


List All of a Device's Startups
````````````````````````````````

This method returns a paginated list of all times that a device reported a vehicle starting up in chronological order.  Included is the vehicle that the device was plugged into at the time.


Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/startups
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "startups": [
          {
            "id" : "a367d821-aad1-4c8a-9446-507898d193f5",
            "timestamp" : "2014-07-23T14:17:18.332Z"
            "vehicleId" : "27b8db50-1274-11e4-9191-0800200c9a66"
          },
          ...
        ],
        "meta": {
          "pagination" : {
            "totalCount" : 14,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/startups?offset=0&limit=10",
              "next" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/startups?offset=10&limit=10",
              "last" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/startups?offset=10&limit=10"
            }
          }
        }
      }


List All of a Device's Shutdowns
````````````````````````````````

This method returns a paginated list of all times that a device reported a vehicle shutting down in chronological order.  Included is the vehicle that the device was plugged into at the time.

Note that this is a raw list as reported by the Device.  There are situations in which the Device will not report an ignition startup or shutdown.  These include times when the Device shutdown in an area without cellular coverage (Underground Parking Garage, for example) or when the device is unplugged immediately before or after vehicle shutdown.

In order to get complete startup and shutdown information, use Trip Services.  Trip Services keeps track of vehicle startups and shutdowns and uses vehicle telemetry data to fill in the times when an explicit startup or shutdown message was not received from a Device.


Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/shutdowns
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "shutdowns": [
          {
            "id" : "f636f4e2-1a5d-4b33-ba16-190d716b95cf",
            "timestamp" : "2014-07-23T16:58:18.332Z"
            "vehicleId" : "27b8db50-1274-11e4-9191-0800200c9a66"
          },
          ...
        ],
        "meta": {
          "pagination" : {
            "totalCount" : 14,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/shutdowns?offset=0&limit=10",
              "next" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/shutdowns?offset=10&limit=10",
              "last" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/shutdowns?offset=10&limit=10"
            }
          }
        }
      }
