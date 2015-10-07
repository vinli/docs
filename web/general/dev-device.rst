Developer Device Authentication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It's important to note that there is no implicit connection between a MyVinli account and a Dev Portal account, even if they share an email address.  In order to preserve a clear separation, MyVinli accounts are treated as wholly different from Dev Portal accounts.

However, as a developer, it's sometimes useful to add a device that you own directly to your application in the Dev Portal before you have a full OAuth flow implemented.  For instance, if you would just like to see the data from a device or play around with the Vinli Platform API, you can use the process below to accomplish this.

Once you have received a Vinli device, the first thing to do is to follow the normal user flow of creating a MyVinli account and adding a device.

1. Create a MyVinli account (https://my.vin.li) and follow the steps to add and name your device.
2. Create a Developer account (https://dev.vin.li).
3. From within the Dev Portal, create an OAuth client.  The type of the client must be `web`, but for the purposes of this process, the `redirectUri` does not have to point to an existing URL.
4. Download the script files and follow the steps in this gist: https://gist.github.com/pkinney/d19ddb46af2ce2270a12.  You will need the credentials that you used to create you MyVinli account and the ID and redirectUri of the Oauth client that you just created.

Once the device is added to your application, you can view the data from the device in the Dev Portal or use the Bearer token returned by step 4 above to access the data using the HTTP API.
