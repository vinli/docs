Internal Transaction Service
============================

Register a Transaction
----------------------

Internal method for registering a transaction...

### Request

      POST /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions
      Content-Type: application/json
      Accept: application/json

      {
        "transaction" : {
          "path" : "/api/v1/devices",
          "service" : "device_service",
          "deviceId" : "7cfdfe90-d65d-11e3-9c1a-0800200c9a66",
          "method" : "POST",
          "statusCode" : 201
        }
      }

### Response

      HTTP/1.1 201 CREATED
      Content-Type: application/json

      {
        "transaction" : {
          "id" : "ef872180-d65d-11e3-9c1a-0800200c9a66"
        }
      }


List Transactions for an Application
------------------------------------

### Request

      GET /api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions
      Accept: application/json

#### Parameters

*since*
*upto*
*limit*
*offset*
*sortBy*
*sortDirection*
*fields*

### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "transactions" : [
          {
            "id" : "ef872180-d65d-11e3-9c1a-0800200c9a66",
            "path" : "/api/v1/devices",
            "timestamp" : 13995199854432
            "service" : "device_service",
            "deviceId" : "7cfdfe90-d65d-11e3-9c1a-0800200c9a66",
            "method" : "POST",
            "statusCode" : 201,
            "links" : {
              "self" : "/api/v1/transactions/ef872180-d65d-11e3-9c1a-0800200c9a66"
            }
          }
          ...
        ],

        "meta" : {
          "totalCount" : 23948,
          "offest" : 0,
          "limit" : 20,
          "links" : {
            "first" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions?since=13995199854432&offset=0&limit=20"
            "next" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions?since=13995199854432&offset=20&limit=20"
            "last" : "/api/v1/_internal/apps/40264af0-d661-11e3-9c1a-0800200c9a66/transactions?since=13995199854432&offset=23940&limit=20"
          }
        }
      }
