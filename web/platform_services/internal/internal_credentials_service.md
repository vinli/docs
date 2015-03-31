Internal Credentials Service
============================

Get Credentials for an App
--------------------------

### Request

      GET /api/v1/_internal/apps/9a107690-d6e2-11e3-9c1a-0800200c9a66/credentials
      Accept: application/json

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "credentials" : {
          "appId" : "9a107690-d6e2-11e3-9c1a-0800200c9a66",
          "apiSecret" : "V1xTt9tYxltCdUU86vhksUuMQOu+lja80YdMy19I"
        }
      }


Get Authentication for a Device
-------------------------------

### Request

      GET /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/deviceAuthorization/e7e3b620-d6e2-11e3-9c1a-0800200c9a66
      Accept: application/json

### Response

If device is authorized:

      HTTP/1.1 204 NO CONTENT

If device is not authorized:

      HTTP/1.1 404 NOT FOUND
