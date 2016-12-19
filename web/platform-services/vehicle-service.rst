Vehicle Service
-----------------

Vinli keeps track of which vehicle a device is or has been plugged into and provides detailed information regarding the specifics about the vehicle.  This gives your application the chance to better personlize the experience of a user as well as the information necessary to classify users and their data by vehicle.  You are only allowed to see vehicles that are associated with a device to which you're application has access.

Vehicle-device assocation is time-based.  A device that is plugged into one vehicle will be associated with that vehicle until it is plugged into a differnt vehicle.  Vinli keeps track of this history for you.  In the case of a device that is shared between multiple vehicles, the same vehicle will appear multiple times in the history.

Note that when a vehicle is first added to the system (when a Vinli device is plugged into a specific vehicle for the first time), only the VIN number is available.  At some point in time after this, Vinli will update the vehicle information with Year, Make, Model, and Trim in addition to even more detailed information (available through the Vehicle's "self" link).


List All of a Device's Vehicles
```````````````````````````````


Returns the vehicles associated with the given device in time series order.


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
      "vehicles": [
        {
          "id": "67e1e940-d6da-11e3-9c1a-0800200c9a66",
          "vin": "2B4GP44R6WR942762",
          "make": "Honda",
          "model": "CR-V",
          "year": "2010",
          "trim": "EX-L 4dr SUV w/Navigation (2.4L 4cyl 5A)",
          "data": {
            "engine": {
              "name": "Engine",
              "equipmentType": "ENGINE",
              "availability": "STANDARD",
              "compressionRatio": 10.5,
              "cylinder": 4,
              "size": 2.4,
              "displacement": 2354,
              "configuration": "inline",
              "fuelType": "regular unleaded",
              "horsepower": 180,
              "torque": 161,
              "totalValves": 16,
              "type": "gas",
              "code": "4INAG2.4",
              "compressorType": "NA",
              "rpm": {
                "horsepower": 6800,
                "torque": 4400
              },
              "valve": {
                "timing": "variable valve timing",
                "gear": "double overhead camshaft"
              }
            },
            "engineDisplacement": 2354,
            "transmission": {
              "name": "5A",
              "equipmentType": "TRANSMISSION",
              "availability": "STANDARD",
              "transmissionType": "AUTOMATIC",
              "numberOfSpeeds": "5"
            },
            "manufacturer": null,
            "categories": {
              "market": "Crossover",
              "EPAClass": "Sport Utility Vehicles",
              "vehicleSize": "Compact",
              "crossover": "Car",
              "primaryBodyType": "SUV",
              "vehicleStyle": "4dr SUV",
              "vehicleType": "SUV"
            },
            "epaMpg": {
              "highway": "28",
              "city": "21"
            },
            "drive": "front wheel drive",
            "numDoors": "4"
          },
          "createdAt": "2016-06-08T20:56:33.033Z",
          "links": {
            "self": "https://platform.vin.li/api/v1/vehicles/38ef2962-7fd2-4319-8389-f9a6b85a7e3f",
            "trips": "https://trips.vin.li/api/v1/vehicles/38ef2962-7fd2-4319-8389-f9a6b85a7e3f/trips",
            "codes": "https://diagnostic.vin.li/api/v1/vehicles/38ef2962-7fd2-4319-8389-f9a6b85a7e3f/codes",
            "collisions": "https://safety.vin.li/api/v1/vehicles/38ef2962-7fd2-4319-8389-f9a6b85a7e3f/collisions"
          },
          "lastStartup": "2016-12-19T14:12:19.476Z"
        },
        {
          "id" : "67e1e940-d6da-11e3-9c1a-0800200c9a66",
          "year" : "2007",
          "make" : "Toyota",
          "model" : "Camry",
          "trim" : "SE V6",
          "vin" : "2B4GP44R6WR942762",
          "data" : {
            "engine": {
              "id": "200373059",
              "name": "Engine",
              "equipmentType": "ENGINE",
              "availability": "STANDARD",
              "compressionRatio": 10.6,
              "cylinder": 4,
              "size": 1.8,
              "displacement": 1798,
              "configuration": "inline",
              "fuelType": "regular unleaded",
              "horsepower": 140,
              "torque": 128,
              "totalValves": 16,
              "type": "gas",
              "code": "4INAG1.8",
              "compressorType": "NA",
              "rpm": {
                "horsepower": 6500,
                "torque": 4300
              },
              "valve": {
                "timing": "variable valve timing",
                "gear": "single overhead camshaft"
              }
            },
            "engineDisplacement": 1798,
            "transmission": null,
            "manufacturer": null,
            "categories": {
              "market": "N/A",
              "EPAClass": "Compact Cars",
              "vehicleSize": "Compact",
              "primaryBodyType": "Car",
              "vehicleStyle": "Sedan",
              "vehicleType": "Car"
            },
            "epaMpg": {
              "highway": "39",
              "city": "28"
            },
            "drive": "front wheel drive",
            "numDoors": "4"
          },
          "createdAt": "2016-08-08T21:12:18.692Z",
          "links": {
            "self": "https://platform-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66",
            "trips": "https://trips-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/trips",
            "codes": "https://diagnostic-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/codes",
            "collisions": "https://safety-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/collisions"
          },
          "lastStartup": "2016-08-08T21:12:16.828Z"
        }
      ],
      "meta": {
        "pagination": {
          "total": 2,
          "limit": 20,
          "offset": 0,
          "links": {
            "first": "https://platform.vin.li/api/v1/devices/60599e46-e221-4df7-8bc6-077c9538141d/vehicles?limit=20&offset=0",
            "last": "https://platform.vin.li/api/v1/devices/60599e46-e221-4df7-8bc6-077c9538141d/vehicles?limit=20&offset=0"
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
          "data" : {
            "engine": {
              "id": "200373059",
              "name": "Engine",
              "equipmentType": "ENGINE",
              "availability": "STANDARD",
              "compressionRatio": 10.6,
              "cylinder": 4,
              "size": 1.8,
              "displacement": 1798,
              "configuration": "inline",
              "fuelType": "regular unleaded",
              "horsepower": 140,
              "torque": 128,
              "totalValves": 16,
              "type": "gas",
              "code": "4INAG1.8",
              "compressorType": "NA",
              "rpm": {
                "horsepower": 6500,
                "torque": 4300
              },
              "valve": {
                "timing": "variable valve timing",
                "gear": "single overhead camshaft"
              }
            },
            "engineDisplacement": 1798,
            "transmission": null,
            "manufacturer": null,
            "categories": {
              "market": "N/A",
              "EPAClass": "Compact Cars",
              "vehicleSize": "Compact",
              "primaryBodyType": "Car",
              "vehicleStyle": "Sedan",
              "vehicleType": "Car"
            },
            "epaMpg": {
              "highway": "39",
              "city": "28"
            },
            "drive": "front wheel drive",
            "numDoors": "4"
          },
          "createdAt": "2016-08-08T21:12:18.692Z",
          "links": {
            "self": "https://platform-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66",
            "trips": "https://trips-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/trips",
            "codes": "https://diagnostic-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/codes",
            "collisions": "https://safety-dev.vin.li/api/v1/vehicles/67e1e940-d6da-11e3-9c1a-0800200c9a66/collisions"
          },
          "lastStartup": "2016-08-08T21:12:16.828Z"
        }
      }