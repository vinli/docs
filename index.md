## Overview
Here you'll find the documentation of all the ways your applications can interact with the Vinli Platform and Device. Included are instructions for developing applications on the Web and mobile devices.

Have any questions or find something we missed? Let us know by filing an issue on this repository.
The documentation is split between platform:

* Web API - straight-forward HTTP API for working with the platform. All of the other SDKs use this API exclusively when talking to the platform.
* iOS SDK
* Android SDK
* Windows Phone SDK - Coming Soon!

We discuss below a few things that are consistent across all of the platforms.

## Vehicle Parameters
The basic "currency" of all of the Vinli's services are the vehicle parameters read and transmitted by the Vinli Device.

The rate at which each parameter is read from the vehicle is curated by the Vinli Device based on what parameters the vehicle provides as well as a set priority of parameters based on what is most useful and most frequently changing. While each vehicle is slightly different in the parameters that are made available, most of your user's vehicles will transmit similar high-frequency parameters.

Note: It is possible to change the priority of parameters for Vinli Enterprise devices. Please contact your Vinli representative for more information.

### Parameter Identification
The Vinli platform provides a consistent naming system for parameters along with lookup tables for human-readable information that you can share with your users.

[https://dev.vin.li/parameters.json]

Each parameter is referenced by a "CamelCase" key throughout the platform. Lookup up this key inside of te

* name - English name of the parameter (i.e. "Calculated Load Value")
* description - text describing the parameter in more detail
* dataType - the type of data the parameter contains (one of "decimal" or "string")
* units - if the type is "decimal" the units of the parameter as it is reported by the system (i.e. vehicleSpeed is reported in "kph", calculatedLoadValue is reported in "%"), otherwise undefined.

### High-Frequency Parameters
The high-frequency parameters sent by a Vinli Device are those that are most related to the "driving behavior" factors. These include:

* rpm
* vehicleSpeed
* calculatedLoadValue
* relativeThrottlePosition
* relativeAcceleratorPosition
* location
* acceleration

The actual frequency of collection for these parameters will vary from as low as every 5 seconds to every 200 milliseconds.

### Low-Frequency Parameters
The remainder of the parameters that the vehicle provides are reported at a much lower frequency. These may include things such as:

* engineCoolantTemp
* fuelPressure
* fuelLevelInput
* ambientAirTemperature
* etc.

These parameters are reported as often as once every 10 seconds or as seldom as once very 5 minutes.

## Api Transactions
Vinli keeps track of every action performed on behalf of your application within the Vinli Platform. This includes calls made by the SDKs and the Developer Portal*. We hold on to each transaction's time, the specific service used, the Device associated with the call (if there is one), and the resulting HTTP code. You can access this information via the Web API's Platform Services.

Note that any requests to the API that are authenticated as your application and result in a 200- or 400-series HTTP response code (Successful and Client Error) will be counted as a transaction. This means that, for example, requesting telemetry data for a device that does not exist or requesting telemetry with invalid parameters will still count as a transaction for your Application. Any requests that result in a 300- or 500-series HTTP response code (Redirect or Server Error) are not counted.

*The Developer Portal is designed to use the API just like your Application would. In fact, the Vinli Platform purposefully doesn't distinguish between calls made directly by your application and those made by the Developer Portal on behalf of your application.
