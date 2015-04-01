Diagnostic Services
===================
In addition to transmitting real-time vehicle telemetry information, the Vinli Device interrogates the vehicle for the status of the malfunction indicator lamp (MIL) or "Check Engine Light".  If the device detects that the MIL is illuniated, it requests the active diagnostic trouble codes (DTCs) for the vehicle.  All of this inforamtion is sent to the Vinli Platform and can be accessed via the Diagnost Services API.

.. toctree::
   :maxdepth: 1

   dtc-history-service
   dtc-notification-service
   dtc-info-service
