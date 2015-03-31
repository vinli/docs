Internal App Service
====================

List All Applications
---------------------

### Request

      GET /api/v1/_internal/apps
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "apps" : [
          {
            "id" : "40264af0-d661-11e3-9c1a-0800200c9a66",
            "name" : "My Application",
            "links" : {
              "self" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66"
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


Create An Application
---------------------

### Request

      POST /api/v1/_internal/apps
      Accept: application/json
      Content-Type: application/json

      {
        "app" : {
          "name" : "My Application",
          "description" : "This is what my application does"
        }
      }

### Response

      HTTP/1.1 201 Created
      Content-Type: application/json
      Location: /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66

      {
        "app" : {
          "id" : "40264af0-d661-11e3-9c1a-0800200c9a66",
          "name" : "My Application"
          "description" : "This is what my application does",
          "apiSecret" : "vHjyubvOFaSCH59Gu6s7puVs2RXn25elbw70DHne",
          "links" : {
            "self" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66",
            "devices" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/devices",
            "groups" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/groups",
            "transactions" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions"
          }
        }
      }



Get An Application
------------------

### Request

      POST /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "app" : {
          "id" : "40264af0-d661-11e3-9c1a-0800200c9a66",
          "name" : "My Application"
          "description" : "This is what my application does",
          "apiSecret" : "vHjyubvOFaSCH59Gu6s7puVs2RXn25elbw70DHne",
          "links" : {
            "self" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66",
            "devices" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/devices",
            "groups" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/groups",
            "transactions" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions"
          }
        }
      }



Edit an Application
-------------------

### Request

      PUT /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66
      Content-Type: application/json

      {
        "app" : {
          "name" : "My New Application",
          "description" : "This is what my application does now"
        }
      }


### Response

      HTTP/1.1 204 NO CONTENT


Reset and App's API Secret
--------------------------

### Request

      DELETE /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/secret
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "app" : {
          "id" : "40264af0-d661-11e3-9c1a-0800200c9a66",
          "name" : "My Application"
          "description" : "This is what my application does",
          "apiSecret" : "vHjyubvOFaSCH59Gu6s7puVs2RXn25elbw70DHne",
          "links" : {
            "self" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66",
            "devices" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/devices",
            "groups" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/groups",
            "transactions" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions"
          }
        }
      }


Delete an Application
---------------------

### Request

      DELETE /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66

### Response

      HTTP/1.1 204 NO CONTENT


Get the Devices for an Application
----------------------------------

### Request

      GET /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/devices
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
