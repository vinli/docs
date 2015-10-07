Developer Device Authentication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As a developer, it's sometimes useful to add a device that you own directly to your application in the Dev Portal before you have a full OAuth flow implemented.  For instance, if you would just like to see the data from a device registered in MyVinli, you can use the process below to accomplish this.

It's important to note that there is no implicit connection between a MyVinli account and a Dev Portal account that share an email address.  In order to preserve a clear separation, MyVinli accounts are treated as wholly different from Dev Portal accounts.

Once you have received a Vinli device, the first thing to do is to follow the normal user flow of creating a MyVinli account and adding a device.

1. Create a MyVinli account (https://my.vin.li) and follow the steps to add and name your device.
2. Create a Developer account (https://dev.vin.li).
3. From within the Dev Portal, create an OAuth client.  The type of the client must be `web`, but for the purposes of this process, the `redirectUri` does not have to point to an existing URL.
4. Download the script files and follow the steps in this gist: https://gist.github.com/pkinney/d19ddb46af2ce2270a12.
