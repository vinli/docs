Device Service
~~~~~~~~~~~~~~

The root element in all interaction with the Vinli platform is the Device.  Each Vinil device has an associated Device ID by which it is referred to within the platform.  However, before your application can access any data or perform any actions on a Device, it must be authorized by the owner of the device.

Enterprise-level applications, which require specific approval from Vinli, are able to manage a specific block of devices that are "owned" by the application.


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


Register a Device
`````````````````

.. note:: This route is only accessible by Enterprise applications.  Consumer applications gain and lose devices as users authorize access via the OAuth flow in MyVinli.


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

Response
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


Deregister a Device
```````````````````

.. note:: This route is only accessible by Enterprise applications.  Consumer applications gain and lose devices as users authorize access via the OAuth flow in MyVinli.

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
