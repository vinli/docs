Rules
=====

Rules
^^^^^

A Rule contains:

#. a Device identifier
#. a collection of `Boundaries`_ for the Device
#. a state which is always exactly one of:

	- "unevaluated" meaning not enough geospatial data is available
	- "uncovered" meaning at least one of the boundaries conditions is unsatisfied
	- "covered" meaning that all of the boundary conditions are satisfied

A Rule is "covered" when all boundary conditions are true. A Rule is "uncovered" when at least one boundary condition is false. When there is insufficient data to determine whether a Rule is "covered" or "uncovered" the Rule's state is "unevaluated".

When sufficient geospatial data is available to change state, the Rule Service:

- changes the state of the Rule to "covered" or "uncovered", and
- creates either a "rule-entry" or "rule-leave" event for applications

For example, suppose an app establishes a Boundary condition around the home of a vehicle owner. When the owner drives home from work, the Rule Service detects that a geospatial Boundary condition is satisfied, The service sets the Rule state to "covered" and then sends a "rule-entry" event to the app.

Likewise, when the vehicle owner leaves home for work, the Rule Service detects that a geospatial Boundary condition is no longer met. The service sets the Rule state to "uncovered" and then sends a "rule-leave" event to the app.

Applications can subscribe to these events in three ways:

- to the "rule-entry" only
- to the "rule-leave" only
- or to both with "rule-\*"


.. toctree::
   :maxdepth: 1

   rule-services