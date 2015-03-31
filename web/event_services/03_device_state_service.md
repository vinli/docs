Device State Service
--------------------

### Get Current State of A Device

This method returns the current state of a Device in relation to a Rule.  The resulting response contains two properties of note:

* `evalutate` - `true` if the Rule has been evaluated for the given device, `false` if the Rule has not been evaluated.  If `false`, it signifies that since the Rule was created, the Device has not transmitted enough information to evaluate the Rule.  If, for instance, the Rule contains a parametric boundary that contains a vehicle parameter that this Vehicle does not provide (such as `hybridBatteryLife` on a non-hybrid vehicle), the Rule will never be evaluated.

#### Request

      GET https://events.vin.li/api/v1/devices/602c6490-d7a3-11e3-9c1a-0800200c9a66/rules/68d489c0-d7a2-11e3-9c1a-0800200c9a66/state
      Accept: application/json

* `deviceId` - required if the rule is a group rule, but is unnecessary if the rule only points to a device


#### Response


      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "state" : {
          "device" : "602c6490-d7a3-11e3-9c1a-0800200c9a66",
          "rule" : "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
          "evaluated" : true
          "covered" : false
        }
      }
