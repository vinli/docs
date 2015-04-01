## Emergency Contact Service


Vinli's Safety Services provide information to a device as to what to do in the event of a collision.  The device will attempt to send SMS messages to each of the contacts specified here in order of the priority.

A maximum of 5 Emergency Contacts may be associated with a single device.  Each contact is required to have a `priority` set.  This integer will be used to sort the contacts in ascending order in the event of a collision.  An SMS will be sent to each contact in order of ascending priority value (1 first, then 2, etc.).  Priority numbers need not be sequential, but specifying the same priority value for two contact will result in an indeterminate order.

One contact can be labeled as a voice contact.  If the associated Vinli device is equipped with voice call functionality, this contact will be called and will be able to speak with the car's occupants after a collision has been detected.

Note that changes to the Emergency Contacts for a Device will not take effect immediately.  The Device will attempt to load update Emergency Contacts at each startup, but in cases where cellular coverage is not available, it may be several startup before this information can be updated.


### Get a list of Emergency Contacts for a Device

Returns a list of Emergency Contacts for a given device in order of ascending priority value.

#### Request

      GET https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts
      Accept: application/json

#### Response


      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "emergency_contacts" : [
          {
            "id" : "a9beede5-a282-4a94-9a50-9ad8a280570f",
            "name" : "Mom",
            "priority" : 1,
            "voiceContact" : false,
            "phoneNumber" : "+12145551212",
            "links" : {
              "self" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts/a9beede5-a282-4a94-9a50-9ad8a280570f"
            }
          },
          ...
        ],
        "meta" : {
          "pagination" : {
            "total" : 5,
            "offset" : 0,
            "limit" : 5,
            "links" : {
              "first" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts?offset=0&limit=5",
              "last" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts?offset=0&limit=5"
            }
          }
        }
      }



### Create an Emergency Contact for a Device


#### Request


      POST https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts
      Accept: application/json
      Content-Type: application/json

      {
        "emergency_contct" : {
          "name" : "Mom",
          "priority" : 1,
          "phoneNumber" : "+12145551212"
        }
      }


#### Response


      HTTP/1.1 201 CREATED
      Content-Type: application/json
      Location: https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts/a9beede5-a282-4a94-9a50-9ad8a280570f

      {
        "emergency_contct" : {
          "id" : "a9beede5-a282-4a94-9a50-9ad8a280570f",
          "name" : "Mom",
          "priority" : 1,
          "voiceContact" : false,
          "phoneNumber" : "+12145551212",
          "links" : {
            "self" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts/a9beede5-a282-4a94-9a50-9ad8a280570f"
          }
        }
      }



### Update an Emergency Contact for a Device


#### Request


      PUT https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts/a9beede5-a282-4a94-9a50-9ad8a280570f
      Accept: application/json
      Content-Type: application/json

      {
        "emergency_contct" : {
          "name" : "Mom",
          "voiceContact" : true
        }
      }


#### Response


      HTTP/1.1 200 OK
      Content-Type: application/json
      Location: https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts/a9beede5-a282-4a94-9a50-9ad8a280570f

      {
        "emergency_contct" : {
          "id" : "a9beede5-a282-4a94-9a50-9ad8a280570f",
          "name" : "Mom",
          "priority" : 1,
          "voiceContact" : true,
          "phoneNumber" : "+12145551212",
          "links" : {
            "self" : "https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts/a9beede5-a282-4a94-9a50-9ad8a280570f"
          }
        }
      }


### Delete an Emergency Contact


#### Request

      DELETE https://safety.vin.li/api/v1/devices/8b8a1810-d6d8-11e3-9c1a-0800200c9a66/emergency_contacts/a9beede5-a282-4a94-9a50-9ad8a280570f


#### Response

      HTTP/1.1 204 NO CONTENT
