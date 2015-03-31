Trip Services
=============

The Vinli device detects vehicle ignition and shutdown and sends those events to the platform.  From these events, it is possible to organize the telemetry data into logical "Trips" for organizing users' activities in your application.  The Trip Service provides access to a catalog of these Trips by Device or by Vehicle and provides mirrors of the Telemetry Services methods centered around these Trips.

It's important to note that trips are sometimes created asyncrhonously--either because they have to be constructed by post-processing or after bulk data upload for a given device.