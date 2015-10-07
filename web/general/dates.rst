Dates and Times
~~~~~~~~~~~~~~~

Before using Vinli services, it's worth spending some time to discuss date and time formatting.

Submitting Dates
````````````````

As part of URLs, dates can be submitted in two ways: ISO8601 formatted or Unix Time.  Both are accepted by the platform APIs and will be converted equally.  As an example, the following are all equivalent as far as the Vinli platform is concerned and will retrieve the same set of snapshots (those occuring after 12:32pm CDT on September 7th, 2014):

ISO 8601
++++++++

* `2014-09-07T17:32:57.893Z` -> `https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?since=2014-09-07T17%3A32%3A57.893Z`
* `2014-09-07T17:32:57.893+00:00` -> `https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?since=2014-09-07T17%3A32%3A57.893%2B00%3A00`
* `2014-09-07T12:32:57.893-05:00` -> `https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?since=2014-09-07T12%3A32%3A57.893-05%3A00`

Unix Time
+++++++++

* `1410111177893` -> `https://telemetry.vin.li/api/v1/devices/27a2ac50-d7bd-11e3-9c1a-0800200c9a66/snapshots?since=1410111177893`

There is obviously a lot that could be discussed regarding the benefits and drawbacks of each style of date.  In general, Unix Time is completely unambiguous, is smaller in footprint (for URLs and storage), does not need to be URL encoded, and is available easily in all major lanuganges; however, ISO 8601 is much easier to read and debug as a human.

In either case, Vinli will handle the dates without issue.

Receiving Dates
```````````````

Where possible, Vinli Platform's APIs will return dates as ISO 8601 formatted Strings.  This makes working with the API with debugging tools much easier as the dates will already be easily human-readable.  All major date libraries are able to parse ISO 8601 natively without much fuss.

Pagination metadata that uses the "Stream Pagination", will generally return URLs with Unit Time query parameters.  As stated above, this avoids any issues with URL encoding and provides for slightly smaller URLs.