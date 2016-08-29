The Vinli Platform
==================

Vinli Platform service:

* authenticates your application, Vinli device and
* configures pagination

Authentication using OAUTH 2 is mandatory for all Vinli apps. Apps must authenticate themselves and user actions to use Vinli services.

Vinli paginates data using:

* resource lists for static resources, or
* streams for rapidly changing data

Pagination can alter the format of dates and times. It's an important topic for apps that rely on telemetry data.


.. toctree::
   :maxdepth: 3

   authentication
   dev-device
   pagination
   dates
