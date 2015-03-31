Internal Device Service
=======================


Add a Device to the Inventory
-----------------------------

### Request

      POST /api/v1/_internal/devices
      Accept: application/json
      Content-Type: application/json

      {
        "device" : {
          "id" : "e7e3b620-d6e2-11e3-9c1a-0800200c9a66",
          "links" : {
            "self" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66",
            "apps" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/apps",
            "vehicles" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/vehicles",
            "groups" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/groups"
          }
        }
      }

### Response

      HTTP/1.1 201 Created
      Content-Type: application/json
      Location: /api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66

      {
        "device" : {
          "id" : "e7e3b620-d6e2-11e3-9c1a-0800200c9a66",
          "links" : {
            "self" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66"
            "apps" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/apps"
          }
        }
      }


List All Devices
----------------

### Request

      GET /api/v1/_internal/devices
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "devices" : [
          {
            "id" : "e7e3b620-d6e2-11e3-9c1a-0800200c9a66",
            "links" : {
              "self" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66",
              "apps" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/apps",
              "vehicles" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/vehicles",
              "groups" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/groups"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            ...
          }
        }
      }



Get a Device
------------

### Request

      GET /api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "device" : {
          "id" : "e7e3b620-d6e2-11e3-9c1a-0800200c9a66",
          "links" : {
            "self" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66",
            "apps" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/apps",
            "vehicles" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/vehicles",
            "groups" : "/api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/groups"
          }
        }
      }


List Applications for a Device
------------------------------

### Request

      GET /api/v1/_internal/devices/e7e3b620-d6e2-11e3-9c1a-0800200c9a66/apps
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "apps" : [
          {
            id: "40264af0-d661-11e3-9c1a-0800200c9a66",
            name: "My Application",
            "links" : {
              ...
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            ...
          }
        }
      }


List All Groups for a Device
----------------------------

### Request

      GET /api/v1/_internal/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups
      Accept: application/json


### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        groups: [
          {
            "id" : "8b5f3460-d610-11e3-9c1a-0800200c9a66",
            "name" : "Justice League",
            "appId" : "40264af0-d661-11e3-9c1a-0800200c9a66",
            "links" : {
              "self" : "/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66",
              "devices" : "/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices"
            }
          },
          ...
        ],
        meta: {
          "pagination" : {
            "totalCount" : 14,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups?offset=0&limit=10",
              "last" : "/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups?offset=10&limit=10",
              "last" : "/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups?offset=10&limit=10"
            }
          }
        }
      }

Add a Device-Vehicle Association
--------------------------------

This should only used by the startup worker when it receives a startup message

### Request

      POST /api/v1/_internal/devices/a8fb20e0-d707-11e3-9c1a-0800200c9a66/vehicles
      Accept: application/json
      Content-Type: application/json

      {
        "vehicle" : {
          "vin" : "2B4GP44R6WR941457"
        }
      }

### Response

      HTTP/1.1 201 Created
      Content-Type: application/json
      Location: "/api/v1/vehicles/89dd2000-d707-11e3-9c1a-0800200c9a66"

      {
        "vehicle" : {
          "id" : "89dd2000-d707-11e3-9c1a-0800200c9a66",
          "vin" : "2B4GP44R6WR941457"
          "links" : {
            "self" : "/api/v1/vehicles/89dd2000-d707-11e3-9c1a-0800200c9a66"
          }
        }
      }
