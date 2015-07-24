Authentication
~~~~~~~~~~~~~~

All calls to the Vinli Platform must be authenticated by an Application.  Each Application is assigned an App ID and an App Secret when it is created.  Both of these are required for an API call to be authenticated.

All API calls must occur over HTTP/SSL.  Any call over HTTP will be rejected at the socket level.

Each request must include the App ID and App Secret in the Authentorization header of the request.  This takes the form of a standard BasicAuth header where the App ID is the username and the App Secret is the password.  For example, an Application with the following credentials:

* **App ID:** c87d5be0-2e69-11e4-8c21-0800200c9a66
* **App Secret:** HKLFFoSILb8VHFJD

could request a list of all of its Devices using CURL with

.. code-block:: json

    curl -u c87d5be0-2e69-11e4-8c21-0800200c9a66:HKLFFoSILb8VHFJD https://platform.vin.li/api/v1/devices

and CURL will take care of setting the Authorization header.  Almost all HTTP libraries you will encounter while writing your application handle BasicAuth for you given the username and password.  In case you need to implement it yourself for some reason follow the steps below to generate the header value:

* Combine the App ID and App Secret using a colon - "c87d5be0-2e69-11e4-8c21-0800200c9a66:HKLFFoSILb8VHFJD" in this case
* Encode the string as Base64 (specifically the RFC2045-MIME variant)
* Append "Basic " before the encoded string.

For the example above the Authorization header would be sent as:

.. code-block:: json

    Authorization: Basic Yzg3ZDViZTAtMmU2OS0xMWU0LThjMjEtMDgwMDIwMGM5YTY2OkhLTEZGb1NJTGI4VkhGSkQ=

It should be obvious but bear repeating that your App Secret should be kept safe and rotated often.  You can reset the secret from the App Management page of the Developer Portal.


Authentication for User Actions
```````````````````````````````

Authentication for actions on behalf of users, such as adding their device to your application, is handled using OAuth 2. To get started with the OAuth 2 workflow, developers must first create a client within their app for each platform they would like to support.  This is done via the Developer Portal.  In general, there are two types of OAuth 2 clients, those that expect response tokens and those that expect response codes.

Token clients are those clients that cannot be secured against leaking their secret, e.g. web clients and mobile apps. They are directly granted a token by the authentication service in exchange for their ID, redirect URI, and the user's approval.

Code clients are those clients that can be secured against leaking their secret, e.g. server clients. Code clients use a user-facing component to obtain a code from the authentication service in exchange for their ID, redirect URI, and the user's approval. The user-facing component then hands the code to the secure client. The secure client can then obtain an access token from the authentication service in exchange for its ID, secret, and the authentication code.

To initiate the authentication flow, the client directs the user to `https://auth.vin.li/oauth/authorization/new?client_id={clientId}&redirect_uri={redirectUri}&=response_type={desiredResponseType}`. After user authentication and app approval, the user will be redirected to the provided redirect URI, which must match the redirect URI registered for the client. The requested access token, authentication code, or an error will be in the fragment (after the `#`) portion of the URI.

Vinli SDKs will also provide authentication support to handle the details for clients and ease integration.
