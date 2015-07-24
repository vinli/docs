Overview
========

The API routes provided by the Event Service work in concert to provide both access to the historical events for a Device as well as web-hooks for your App to receive immediate notification when an event occurs.

The normal life-cycle of working with Event Service is:

 * Create a Subscription for a particular event type for a device
 * That event occurs for that device
 * An event is created
 * Event Service looks for all Subscriptions for which this Event qualifies
 * A Notification is created that contains all the relevant information
 * The Notification is POSTed to the URL listed in the Subscription
 * Links within the Notification allow the App to explore the related information directly


Event Types
~~~~~~~~~~~

There are several types of events that the platform will track on a device-by-device basis.  These include:

 * `startup`
 * `shutdown`
 * `rule-enter`
 * `rule-leave`
 * `dtc-code-detect`
 * `dtc-code-clear`
 * `collision`
 * `trip-started`
 * `trip-orphaned`
 * `trip-stopped`
 * `trip-completed`

Objects
~~~~~~~

Almost all events occur in the context of a higher-level object.  For example, startup and shutdown events occur in relation to a given Vehicle, rule-enter and rule-leave events occur in relation to a given Rule.  This information is available as part of the event object property.  Additionally, subscriptions can specifically reference a given object.  For example, a subscription to `startup` events can optionally reference a particular Vehicle; in this way, an App will only be notified of startups where the Device is attached to a particular Vehicle.

NOTE: Subscriptions for event types `rule-enter`, `rule-leave`, or `rule-*` must reference a single Rule.  When creating the subscription, the Rule is checked to ensure that it belongs to this particular device.