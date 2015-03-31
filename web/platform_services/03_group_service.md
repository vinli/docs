Group Service
-------------


Groups belong to one Application and contain multiple devices.  A device may belong to zero, one, or more Groups.

For the most part, Groups are used by the Rules service to simplify applying one Rule to multiple devices.  However, they may also be used as a means of organizing Devices within your application.


### List all Groups


#### Request

      GET https://platform.vin.li/api/v1/groups
      Accept: application/json

#### Response


      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "groups": [
          "id" : "8b5f3460-d610-11e3-9c1a-0800200c9a66",
          "name" : "North Texas Fleet"
          "links" : {
            "self" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66",
            "devices" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices"
          },
          ...
        ],
        meta: {
          "pagination" : {
            "total" : 82,
            "offset" : 0,
            "limit" : 10,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/groups?offset=0&limit=10",
              "last" : "https://platform.vin.li/api/v1/groups?offset=72&limit=10",
              "next" : "https://platform.vin.li/api/v1/groups?offset=10&limit=10"
            }
          }
        }
      }


### Create a Group


#### Request


      POST https://platform.vin.li/api/v1/groups
      Content-Type: application/json
      Accept: application/json

      {
        "group" : {
          "name" : "North Texas Fleet"
        }
      }


#### Response:


      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://platform.vin.li/api/v1/groups/{groupId}

      {
        "group": {
          "id" : "8b5f3460-d610-11e3-9c1a-0800200c9a66",
          "name" : "North Texas Fleet"
          "links" : {
            "self" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66",
            "devices" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices"
          }
        }
      }


### Get a Group


#### Request

      GET https://platform.vin.li/api/v1/groups/{groupId}
      Accept: application/json


#### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "group": {
          "id" : "8b5f3460-d610-11e3-9c1a-0800200c9a66",
          "name" : "North Texas Fleet"
          "links" : {
            "self" : "https://platform.vin.li/api/v1/groups/{groupId}",
            "devices" : "https://platform.vin.li/api/v1/groups/{groupId}/devices"
          }
        }
      }



### Edit a Group

Allows you to rename a Group.  This is purely decorative.

#### Request

      PUT https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66
      Content-Type: application/json

      {
        "group" : {
          "name" : "Oklahoma Fleet"
        }
      }


#### Response

      HTTP/1.1 204 NO CONTENT


### Delete a Group


#### Request

      DELETE https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66


#### Response

      HTTP/1.1 204 NO CONTENT




### Add a Device to a Group


#### Request

      POST https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices
      Content-Type: application/json
      Accept: application/json

      {
        "device" : {
          "id" : "03954440-d618-11e3-9c1a-0800200c9a66"
        }
      }

#### Response

      HTTP/1.1 204 NO CONTENT


### List All of a Group's Devices


#### Request

      GET https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices
      Accept: application/json


#### Response

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
              "first" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices?offset=0&limit=20",
              "last" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices?offset=1420&limit=20",
              "next" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices?offset=20&limit=20"
            }
          }
        }
      }


### List All of a Device's Groups


#### Request

      GET https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups
      Accept: application/json


#### Response

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "groups": [
          {
            "id" : "8b5f3460-d610-11e3-9c1a-0800200c9a66",
            "name" : "North Texas Fleet"
            "links" : {
              "self" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66",
              "devices" : "https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices"
            }
          },
          ...
        ],
        "meta": {
          "pagination" : {
            "totalCount" : 14,
            "limit" : 10,
            "offset" : 0,
            "links" : {
              "first" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups?offset=0&limit=10",
              "next" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups?offset=10&limit=10",
              "last" : "https://platform.vin.li/api/v1/devices/821374c0-d6d8-11e3-9c1a-0800200c9a66/groups?offset=10&limit=10"
            }
          }
        }
      }


### Remove a Device from a Group


#### Request

      DELETE https://platform.vin.li/api/v1/groups/8b5f3460-d610-11e3-9c1a-0800200c9a66/devices/{deviceId}


#### Response

      HTTP/1.1 204 NO CONTENT
