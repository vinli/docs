Vehicle Service
~~~~~~~~~~~~~~~

Vinli keeps track of which vehicle a device is or has been plugged into and provides detailed information regarding thee specifics about the vehicle.  This gives your application the chance to better personlize the experience of a user as well as the information necessary to classify users and their data by vehicle.  You are only allowed to see vehicles that are associated with a device to which you're application has access.

Vehicle-device assocation is time-based.  A device that is plugged into one vehicle will be associated with that vehicle until it is plugged into a differnt vehicle.  Vinli keeps track of this history for you.  In the case of a device that is shared between multiple vehicles, the same vehicle will appear multiple times in the history.

Note that when a vehicle is first added to the system (when a Vinli device is plugged into a specific vehicle for the first time), only the VIN number is available.  At some point in time after this, Vinli will update the vehicle information with Year, Make, Model, and Trim in addition to even more detailed information (available through the Vehicle's "self" link).


List All of a Device's Vehicles
```````````````````````````````


Returns the vehicles associated with the given device in chronological order.


Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles
      Accept: application/json

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicles" : [
          {
            "id" : "67e1e940-d6da-11e3-9c1a-0800200c9a66",
            "year" : "2007",
            "make" : "Toyota",
            "model" : "Camry",
            "trim" : "SE V6",
            "vin" : "2B4GP44R6WR942762",
            "links" : {
              "self" : "https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66",
              "trips" : "https://trip.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/trips",
              "collisions" : "https://safety.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/collisions",
              "reportCards" : "https://behavioral.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/reportCards"
            }
          },
          {
            "id" : "2a88b0f0-d6db-11e3-9c1a-0800200c9a66",
            "vin" : "JE3BW50W4NZ676124",
            "links" : {
              "self" : "https://platform.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66",
              "trips" : "https://trip.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66/trips",
              "collisions" : "https://safety.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66/collisions",
              "reportCards" : "https://behavioral.vin.li/api/v1/vehicles/2a88b0f0-d6db-11e3-9c1a-0800200c9a66/reportCards"
            }
          },
          ...
        ],
        "meta": {
          "pagination" : {
            "total" : 24,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles?offset=0&limit=10",
              "next" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles?offset=10&limit=10",
              "last" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles?offset=20&limit=10"
            }
          }
        }
      }


List a Device's Latest Vehicle
``````````````````````````````


Returns the vehicle most recently associated with the given device if it exists.  If the device has not been associated with a vehicle, a null vehicle object is returned.

Basic vehicle information is returned as part of this response.  Follow the vehicle's "self" link to get full detailed information about the vehicle.

Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/vehicles/_latest
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicle" : {
          "id" : "67e1e940-d6da-11e3-9c1a-0800200c9a66",
          "year" : "2007",
          "make" : "Toyota",
          "model" : "Camry",
          "trim" : "SE V6",
          "vin" : "2B4GP44R6WR942762",
          "links" : {
            "self" : "https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66",
            "trips" : "https://trip.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/trips",
            "collisions" : "https://safety.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/collisions",
            "reportCards" : "https://behavioral.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/reportCards"
          }
        }
      }


Get Information About a Vehicle
```````````````````````````````

Returns detailed information about a vehicle.  This may include, but is not limitted to:

* Year
* Make
* Model
* Trim
* Engine Information
* Transmission Information
* Available Options


Request
+++++++

.. code-block:: json

      GET https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "vehicle" : {
          "id" : "67e1e940-d6da-11e3-9c1a-0800200c9a66",
          "year" : "2007",
          "make" : "Toyota",
          "model" : "Camry",
          "trim" : "SE V6",
          "vin" : "2B4GP44R6WR942762",
          "data" : { ... },
          "links" : {
            "self" : "https://platform.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66"
          }
        }
      }
