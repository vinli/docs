Trip Tagging Service
====================

Trip Tagging Service allows developers to attach Tags to trips. Generally, tags are a good way to help users define, segment, and identify their trips.

Tag Properties
``````````````
Since Tags are designed to serve as a simple yet flexible categorization system for Trips, there are only a few Tag properties:
* `name` - Required. A string that serves as the user facing label. `name` is unique to each tag, so you shouldn't have multiple "charity" tags for the same trip.
* `percentage` - Required. A float value, that indicated the percentage of the trip to which the tag applies. Defaults to 100.0

Create Tags for a Trip
``````````````````````
This route allows you to create one or many tags for a Trip.

Request
+++++++

.. code-block:: json

      POST https://trip-tags.vin.li/api/v1/tags
      Accept: application/json
      
      Body:
      {
        "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
        "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
        "tags": [{
          "percentage": 50.0,
          "name": "business"
        },
        {
          "percentage": 10.0,
          "name": "personal"
        },
        {
          "percentage": 40.0,
          "name": "mixed",
          "appMeta": {
  	        "personal-miles": 6,
   	        "business-miles": 42,
		"comments": "Hello world"
	    }
        }]
      }

Response
++++++++

.. code-block:: json

     	HTTP/1.1 201 CREATED
	{
	  "tags": [
	    {
	      "id": "00998c51-2d47-4289-a6a0-15038e81e5f5",
	      "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
	      "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
	      "name": "Business",
	      "percentage": 50,
	      "appMeta": {},
	      "created_at": "2017-09-06T16:53:12.057208Z",
	      "updated_at": "2017-09-06T16:53:12.057208Z"
	    },
	    {
	      "id": "f934b061-3d33-426e-8dad-14b199be33b9",
	      "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
	      "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
	      "name": "Personal",
	      "percentage": 10,
	      "appMeta": {},
	      "created_at": "2017-09-06T16:53:12.057208Z",
	      "updated_at": "2017-09-06T16:53:12.057208Z"
	    },
	    {
	      "id": "dcdeb417-80b9-43c9-ac41-3d4e4abf896c",
	      "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
	      "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
	      "name": "Mixed",
	      "percentage": 40,
	      "appMeta": {
		"business-miles": 42,
		"comments": "Hello world",
		"personal-miles": 6
	      },
	      "created_at": "2017-09-06T16:53:12.057208Z",
	      "updated_at": "2017-09-06T16:53:12.057208Z"
	    }
	  ]
	}

Get Tags for a Trip
```````````````````

This route returns a list of all tags associated with a given trip.


Request
+++++++

.. code-block:: json

      GET https://trip-tags.vin.li/api/v1/trips/c2d369a3-0e98-4a29-841e-48ed64dd473d/tags
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK

      {
        "tags": [
          {
            "id": "4ef45376-6607-47c0-b21b-ed88aef1f99d",
            "name": "business",
            "percentage": 65.0,
            "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
            "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
            "createdAt": "2017-07-19T20:45:49.749861Z",
            "updatedAt": "2017-07-22T09:43:45.749582Z"
          },
          {
            "id": "4ef45376-6607-47c0-b21b-ed88aef1f99d",
            "name": "personal",
            "percentage": 35.0,
            "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
            "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
            "createdAt": "2017-07-19T20:45:49.749861Z",
            "updatedAt": "2017-07-22T09:43:45.749582Z"
          }
        ],
        "meta": {
          "pagination": {
            "total": 50,
            "limit": 25,
            "offset": 0,
            "links": {
              "first": "http://trip-tags.vin.li/api/v1/trip/28cbf57e-0a63-4120-b652-bf06f6c7b723/tags?offset=0&limit=25",
              "last": "http://trip-tags.vin.li/api/v1/trip/28cbf57e-0a63-4120-b652-bf06f6c7b723/tags?offset=25&limit=25",
              "next": "http://trip-tags.vin.li/api/v1/trip/28cbf57e-0a63-4120-b652-bf06f6c7b723/tags?offset=25&limit=25"
            }
          }
        }
      }


Get a Specific Tag
``````````````````
This route allows you to retreive a specific tag by `tagId`

Request
+++++++

.. code-block:: json

      GET https://trip-tags.vin.li/api/v1/trips/c2d369a3-0e98-4a29-841e-48ed64dd473d/tags/4ef45376-6607-47c0-b21b-ed88aef1f99d
      Accept: application/json


Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK

      {
        "tag": {
          "id": "4ef45376-6607-47c0-b21b-ed88aef1f99d",
          "name": "business",
          "percentage": 65.0,
          "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
          "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
          "createdAt": "2017-07-19T20:45:49.749861Z",
          "updatedAt": "2017-07-22T09:43:45.749582Z"
        }
      }


Update Tags for a Trip
``````````````````````
This route allows you to update percentage values for tags associated with a Trip. Just pass an array of tags with the tag `name` and the new `percentage` value, and Vinli will update `percentage` values for Tags belonging to the trip with matching names.

Request
+++++++

.. code-block:: json

      PUT https://trip-tags.vin.li/api/v1/trips/c2d369a3-0e98-4a29-841e-48ed64dd473d/tags
      Accept: application/json
      
      Body:
      {
        "tags": [{
          "percentage": 40.0,
          "name": "business"
        },
        {
          "percentage": 60.0,
          "name": "personal"
        }]
      }

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK

      {
        "tags": [{
            "id": "4ef45376-6607-47c0-b21b-ed88aef1f99d",
            "name": "business",
            "percentage": 40.0,
            "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
            "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
            "createdAt": "2017-07-19T20:45:49.749861Z",
            "updatedAt": "2017-07-21T18:15:49.582045Z"
          },
          {
          "id": "4ef45376-6607-47c0-b21b-ed88aef1f99d",
          "name": "personal",
          "percentage": 60.0,
          "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
          "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
          "createdAt": "2017-07-19T20:45:49.749861Z",
          "updatedAt": "2017-07-21T18:15:49.582045Z"
        }]
      }

Update a Specific Tag
`````````````````````
This route allows you to update the `name` and/or `percentage` values for a specific Tag.

Request
+++++++

.. code-block:: json

      PUT https://trip-tags.vin.li/api/v1/tags/4ef45376-6607-47c0-b21b-ed88aef1f99d
      Accept: application/json
      Body:
      {
        "name": "medical",
        "percentage": 100.0
      }

Response
++++++++

.. code-block:: json

      HTTP/1.1 200 OK

      {
        "tag": {
          "id": "4ef45376-6607-47c0-b21b-ed88aef1f99d",
          "name": "medical",
          "percentage": 100.0,
          "deviceId": "c08394e5-78f8-4621-b962-269c1e65ab71",
          "tripId": "c2d369a3-0e98-4a29-841e-48ed64dd473d",
          "createdAt": "2017-07-19T20:45:49.749861Z",
          "updatedAt": "2017-07-22T09:43:45.749582Z"
        }
      }


Delete a Specific Tag
`````````````````````
Delete a Tag with this route. A 204 response will be provided upon successful deletion.

Request
+++++++

.. code-block:: json

      DELETE https://trip-tags.vin.li/api/v1/trips/c2d369a3-0e98-4a29-841e-48ed64dd473d/tags/4ef45376-6607-47c0-b21b-ed88aef1f99d


Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT


Delete All Tags for a Trip
``````````````````````````
This route deletes all tags associated with a Trip, and is handy if you need to "wipe the slate clean" when it comes to tagging for the trip at hand.

Request
+++++++

.. code-block:: json

      DELETE https://trip-tags.vin.li/api/v1/trips/c2d369a3-0e98-4a29-841e-48ed64dd473d/tags


Response
++++++++

.. code-block:: json

      HTTP/1.1 204 NO CONTENT




.. toctree::
  :maxdepth: 2
