Rule Services
==============

Rules
~~~~~

A Rule is a set of conditions (Boundaries) specified for a particular Device.  Each Rule is evaluated when sufficient data is available for the corresponding Device.  The state of a Rule as it pertains to a particular Device is maintained by the Rule Service.  When the Boundaries of a Rule are breached (in either direction), a `rule-leave` or `rule-entry` event is created.  These events can be subscribed to as a specific direction (`rule-leave` or `rule-entry`) or in either direction (`rule-*`).


In a nutshell:

* Rules consist of one or more Boundaries.
* Rules start off as "unevaluated"
* Rules are evaluated as soon as enough recent information is available from a device.  For instance, if a device
* Rules are either in a state of "covered" (meaning that all the boundaries are satisfied), "uncovered" (meaning that not all of the boundaries are satisfied), or "unevaluated"
* If a Rule changes state from "covered" to "uncovered" or vice versa (or from "unevaluated" to either "covered" or "uncovered"), an event is created within the Event Service.


Boundaries
~~~~~~~~~~

Rules consist of one or more Boundaries (individual conditions), and each of these boundaries can be either "parametric" or "geospatial."  A geospatial boundary, as the name suggests, is one that defines a specific area on the surface of the Earth.  This is referenced by a single point and a radius, thus defining a particular circular area on the planet, or by a polygon.  A parametric boundary is one that defines a specific range for a particular vehicle parameter (i.e. RPM between 2000 and 4000).  Parametric boundaries may also be open-ended (i.e. RPM greater than 3500).

The boundaries are evaluated in an "all-or-none" manner, meaning that the rule is covered when all of the boundaries are met, and when any of the Boundaries are not met, the rule is uncovered.  In other words, a Rule is evaluated by ANDing the results of its component Boundaries.

There are a few important considerations when constructing the boundaries for a given rule:

* A rule must have at least one boundary.
* A rule may not have more than one boundary for a given parameter.  Since the rules are evaluated in an "all-or-none" manner, having two non-overlapping boundaries for the same parameter would cause the rule never to be evaluated as "covered."
* For the same reason, a rule may have no more than one geospatial boundary (or none at all).