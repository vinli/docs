Authentication
==============

Apps must authenticate through Vinli Platform services. When you register an app at `dev.vin.li`_, the Vinli Platform assigns a unique App ID and App Secret. Your app will need both, to authenticate with Vinli services.

All API calls must use HTTP/SSL. Vinli will reject all plain HTTP calls at the socket level.

Application Authentication
---------------------------

Each request must include the App ID and App Secret in the Authorization header of the request.  This takes the form of a standard BasicAuth header where the App ID is the username and the App Secret is the password.  For example, an Application with the following credentials:

* **App ID:** c87d5be0-2e69-11e4-8c21-0800200c9a66
* **App Secret:** HKLFFoSILb8VHFJD

could request a list of all of its Devices using CURL with

.. code-block:: json

    curl -u c87d5be0-2e69-11e4-8c21-0800200c9a66:HKLFFoSILb8VHFJD https://platform.vin.li/api/v1/devices

and CURL will take care of setting the Authorization header.  Almost all HTTP libraries can handle BasicAuth for you, as long as you have a username and password.

If you must implement BasicAuth yourself, follow the steps below to generate the header value:

#. Combine the App ID and App Secret using a colon. Ex: c87d5be0-2e69-11e4-8c21-0800200c9a66:HKLFFoSILb8VHFJD
#. Encode the string as Base64 (specifically the RFC2045-MIME variant).
#. Prepend the string "Basic " (note the space after the word 'Basic') to the the encoded string.

For the example above, the Authorization header would be sent as:

.. code-block:: json

    Authorization: Basic Yzg3ZDViZTAtMmU2OS0xMWU0LThjMjEtMDgwMDIwMGM5YTY2OkhLTEZGb1NJTGI4VkhGSkQ=


**Important:** the App Secret should be kept safe and rotated often. You can reset the App Secret from the App Management page of the Developer Portal at `dev.vin.li`_.


User Action Authentication
--------------------------

Vinli services require user actions to authernticate with OAuth 2. Developers must register their apps for each platform they would like to support. at `dev.vin.li`_.

In general, there are two types of OAuth 2 clients, those that expect response tokens and those that expect response codes.

Vinli supports two OAuth 2 flows:

* Implicit Grant Flow is used for clients that cannot secure their App Secret. For example, web clients and mobile apps.
* Authorization Code Flow is used for clients that can be secured against leaking their App Secret. For example, server clients or clients that require long-lived access.

Implicit Grant Flow clients are directly granted a token by the authentication service in exchange for their ID, redirect URI, and the user's approval.

Authorization Code clients use a user-facing component to obtain a code from the authentication service in exchange for their ID, redirect URI, and the user's approval. The user-facing component then hands the code to the secure client. The secure client can then obtain an access token from the authentication service in exchange for its ID, secret, and the authentication code.

To initiate the authentication flow, the client directs the user to:

.. code-block:: json

	https://auth.vin.li/oauth/authorization/new?client_id={clientId}&redirect_uri={redirectUri}&response_type={desiredResponseType}

After user authentication and app approval, the app should redirect to the provided redirect URI, which must match the redirect URI registered for the client. The requested access token, authentication code, or an error will be in the fragment (after the `#`) portion of the URI.

.. _dev.vin.li: https://dev.vin.li/
