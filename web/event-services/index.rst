Event Services
===================
The set of tools provided by Vinli's Event Services allows an application to create and manage complex sets of Rules that are evaluated on particular devices or groups of devices.  These Rules are constructed using the parameters provided by the Vinli device.  More information about these parameters can be found in the "Parameters" section above, but it's important to not that only those parameters with a decimal `dataType` are usable in Rules.

As data is streamed from the Vinli device to the platform, each snapshot is evaluated by the Event Service to see if the new information causes the device to leave or enter the boundaries of a given rule.  This can get a bit complicated, especially as the rules your application need grow.  The important thing to remember is that a Rule represents a continuity of states that the vehicle is either inside of (covered) or outside of (not covered).

.. toctree::
   :maxdepth: 1

   overview
   events
   subscriptions
   notifications
