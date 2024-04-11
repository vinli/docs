Locations
----------

Returns the latest `limit` number of points of the device's location before or at the `until` time and after the `since` time. If the `until` time is not specified, then the service will return snapshots until the current time when the call is made. The `location` property contains a valid GeoJSON FeatureCollection object consisting of Point features for each location. The timestamp for each location is the in the `properties` field of the feature.

Additionally, selected or all parameters that were recorded at each location can also be included in the `properties` field. When `all` is specified, this method acts just like the Device Messages method below, but it is formatted as valid GeoJSON.


Request
+++++++

::
	
      GET https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/locations?fields=rpm,vehicleSpeed
      Accept: application/json

* `fields` - Can be `all` or a comma-separated list of parameter keys to be included in the `properties` field.
* `until` - Results will contain snapshots whose timestamps are less than or equal to the `until` value. If an `until` value is not specified, the current time when the call is made will be used as the `until` value.
* `since` - Results will contain snapshots whose timestamps are greater than the `since` value. If a `since` value is not specified, no lower limit will be placed on the returned snapshots.
* `limit` - Results will contain no more than `limit` number of snapshots


Response
++++++++

::
	
      {
        "locations" : {
          "type" : "FeatureCollection",
          "features" : [
            {
              "type" : "Feature",
              "geometry" : {
                "type" : "Point",
                "coordinates" : [-90.0811, 29.9508]
              },
              "properties" : {
                "timestamp" : "2014-03-13T17:54:20.050Z",
                "rpm" : 1264,
                "vehicleSpeed" : 54
              }
            },
            {
              "type" : "Feature",
              "geometry" : {
                "type" : "Point",
                "coordinates" : [-90.08198, 29.9498]
              },
              "properties" : {
                "timestamp" : "2014-03-13T17:54:07.122Z",
                "rpm" : 1832
              }
            },
            ...
          ]
        },
        "meta" : {
          "pagination" : {
            "remaining": 469,
            "until": "2016-12-20T00:02:36.644Z",
            "since": "1970-01-01T00:00:00.000Z",
            "limit": 3,
            "sortDir": "desc",
            "links" : {
              "prior" : "https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/locations?until=1394733247121"
            }
          }
        }
      }