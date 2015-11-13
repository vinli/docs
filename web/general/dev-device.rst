Developer Device Authentication
--------------------------------

There is no connection between a MyVinli account and a Dev Portal account, even if they share an email address.

However, it can be useful to add a device to your application, before you have a full OAuth flow implemented.  After adding a device, you can inspect data from a device or experiment with the Vinli Platform API.

Follow the procedure below to add a device to your app:

1. Create a `MyVinli`_ account and follow the steps to add and name your device.
2. Create a `Vinli Developer`_ account.
3. From the Vinli Developer Portal, create an OAuth client. The Client Type should be set to Web. For the purposes of this procedure, the Redirect URI does not have to point to an existing URL.
4. Download the script files and follow the steps in this `gist`_. Use your MyVinli credentials, the ID and Redirect URI of the Oauth client that you created in step 3.

After adding the device, you can view the device data in the Dev Portal. You can also use the Bearer token, returned by step 4, to access device data using the HTTP API.

.. _MyVinli: https://my.vin.li
.. _Vinli Developer: https://dev.vin.li
.. _gist: https://gist.github.com/pkinney/d19ddb46af2ce2270a12
