Boundaries
==========

A Boundary is either:

- a geospatial boundary that defines a region on the Earth's surface, or
- a parametric boundary that defines a range for some vehicle parameter

A geospatial boundary defines a circular geographic region by specifying:

- a single geographic point, and
- a radius in meters

A parametric boundary specifies either:

- a bounded range, such as "RPM between 2000 and 4000", or
- an unbounded range, such as "RPM greater than 3500"

A Rule is "covered" when all Boundary conditions are true. This fact has important implications for rule design.

- Suppose an app developer adds two disjoint geospatial boundaries to a rule. The rule can never enter the "covered" state nor ever fire a "rule-entry" or "rule-leave" event. It will forever remain in the "unevaluated" state. Because the Device can only be in one location at a time, at best it can only satisfy one of the boundary conditions but never both.
- Similarly, a rule will never fire an event if the rule contains two disjoint parametric boundaries for the same vehicle parameter. For example, "RPM greater than 3500" and "RPM less than 2000" will forever remain in the "unevaluated" state.

Because of these implications, the Rule Service allows at most one geospatial boundary in a Rule. This eliminates the problem of disjoint geospatial regions. However, app developers must still avoid creating disjoint parametric boundaries.


.. toctree::
   :maxdepth: 1

   rule-services