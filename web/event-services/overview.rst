Event Services
==============

Rules
~~~~~

A Rule is a set of conditions (Boundaries) specified for a particular Device or Group.  Each Rule is evaluated when sufficient data is available for the corresponding Device or a member of the corresponding Group.  The state of a Rule as it pertains to a particular Device is maintained by the Event Services.  (This can be queried using the Device State Service described below.)  When creating a Rule, your application must include a URL that will be called when the state of the Rule for a particular device changes.


In a nutshell:

* Rules consist of one or more Boundaries.
* Rules start off as "unevaluated"
* Rules are evaluated as soon as enough recent information is available from a device.  For instance, if a device
* Rules are either in a state of "covered" (meaning that all the boundaries are satisfied), "uncovered" (meaning that not all of the boundaries are satisfied), or "unevaluated"
* If a Rule changes state from "covered" to "uncovered" or vice versa, the notification settings on the rule are used to notify your application of the state change.


Boundaries
~~~~~~~~~~

Rules consist of one or more Boundaries (individual conditions), and each of these boundaries can be either "parametric" or "geospatial."  A geospatial boundary, as the name suggests, is one that defines a specific area on the surface of the Earth.  This is referenced by by a single point and a radius, thus defining a particular circular area on the planet.  A parametric boundary is one that defines a specific range for a particular vehicle parameter (i.e. RPM between 2000 and 4000).  Parametric boundaries may also be open-ended (i.e. RPM greater than 3500).

The boundaries are evaluated in an "all-or-none" manner, meaning that the rule is covered when all of the boundaries are met, and when any of the Boundaries are not met, the rule is uncovered.  In other words, a Rule is evaluated by ANDing the results of its component Boundaries.

There are a few important considerations when constructing the boundaries for a given rule:

* A rule must have at least one boundary.
* A rule may not have more than one boundary for a given parameter.  Since the rules are evaluated in an "all-or-none" manner, having two non-overlapping boundaries for the same parameter would cause the rule never to be evaluated as "covered."
* For the same reason, a rule may have no more than one geospatial boundary (or none at all).


Notifications
~~~~~~~~~~~~~

When a device moves from being covered by a rule to being not covered (or vice versa), an event is generated and a notification is triggered.  The `notificationUrl` of the rule is called via POST with a payload containing data regarding the event, rule, device, and snapshot that generated the notification.  The following is an example of the payload submitted for a particular rule (in this example this would have been POSTed to https://api.myapp.com/vinli_notifications):

.. code-block:: json

    {
      "snapshot": {
        "messageId" : "2f11d630-141e-11e4-b717-5977b6c38d23",
        "timestamp": 1401307900001,
        "parameters": {
          "vehicleSpeed": 145
        },
        "links" : {
          "self" : "https://telemetry.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b6400/messages/2f11d630-141e-11e4-b717-5977b6c38d23"
        }
      },
      "rule": {
        "id": "68d489c0-d7a2-11e3-9c1a-0800200c9a66",
        "name": "Speed over 70mph",
        "links": {
          "self": "https://events.vin.li/api/v1/rules/9244d870-141d-11e4-a15c-a5694c3ebd21"
        },
        "notificationUrl": "https://api.myapp.com/vinli_notifications",
        "notificationMetadata": {
          "userFirstName": "John",
          "userLastName": "Sample",
          "smsPhoneNumber": "2145551212"
        }
      },
      "deviceId": "fe4bbc20-cc90-11e3-8e05-f3abac5b6400",
      "direction": "leave"
    }


* `snapshot` - the vehicle telemetry that triggered the notification including the parameters that specifically violated the rule.  In the case above, while there would have been more parameters sent as part of this message, only the `vehicleSpeed` parameter was included.  A link to the message in its entirety is included for more detail.
* `rule` - representation of the rule itself that was triggered.  Note that this contains whatever metadata was created with the rule.
* `deviceId` - the ID of the device that triggered the notification
* `direction` - the direction in which the device crossed the boundary.  If the rule was in a "covered" state for this device and is now not "covered," the direction will be `leave`.  If the opposite is true, the direction will be `enter`.