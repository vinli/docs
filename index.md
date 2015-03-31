## Overview
Here you'll find the documentation of all the ways your applications can interact with the Vinli Platform and Device. Included are instructions for developing applications on the Web and mobile devices.

Have any questions or find something we missed? Let us know by filing an issue on this repository.

## Vehicle Parameters
### Parameter Identification
### High-Frequency Parameters
### Low-Frequency Parameters

## Api Transactions
Vinli keeps track of every action performed on behalf of your application within the Vinli Platform. This includes calls made by the SDKs and the Developer Portal*. We hold on to each transaction's time, the specific service used, the Device associated with the call (if there is one), and the resulting HTTP code. You can access this information via the Web API's Platform Services.

Note that any requests to the API that are authenticated as your application and result in a 200- or 400-series HTTP response code (Successful and Client Error) will be counted as a transaction. This means that, for example, requesting telemetry data for a device that does not exist or requesting telemetry with invalid parameters will still count as a transaction for your Application. Any requests that result in a 300- or 500-series HTTP response code (Redirect or Server Error) are not counted.

*The Developer Portal is designed to use the API just like your Application would. In fact, the Vinli Platform purposefully doesn't distinguish between calls made directly by your application and those made by the Developer Portal on behalf of your application.
