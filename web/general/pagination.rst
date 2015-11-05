Pagination
==========

Vinli APIs paginate all list responses. Pagination varies slightly depending on the type of data being returned:

* resource lists for relatively static resources (devices, groups, etc.)
* streams for rapidly changing data (telemetry, location, etc.)


Resource List Pagination
-------------------------

This pagination uses `offset` and `limit` to page through a sorted lists of objects.  By default this sorting is based on the creation time and is sorted in reverse chronological order, i.e. time series order. The first item in the list is the most recent. This order can be modified using the `sortBy` and `sortDirection` parameters.  As part of the `meta` property's `pagination` field in the response, the API will return:

 * `count` - the total number of items available regardless of pagination
 * `limit` - the limit used for the list returned (This will be the limit requested by the client unless one was not passed, in which case the default for this method will be returned, or unless the limit requested by the client was larger than the max allowed for the method, in which case the maximum allowable limit will be returned)
 * `offset` - the offset used for the list returned (This will be the offset requested by the client unless one was not passed in the call, in which case 0 will be returned)
 * `links` - an object containing URLs for traversing the pages of the list
   * `first` - URL for the first page
   * `last` - URL for the last page
   * `next` - URL for the next page (If the current page is the last page, this field will not be returned.)
   * `prev` - URL for the previous page (If the current page is the first page, this field will not be returned.)

Pagination is done within the context of any other URL parameters passed.  For instance, if a client requests transactions since January 1st, 2014 until February 1st, 2014 in chronological order, passing an `offset` of 0 will return the transactions starting on January 1st.  Incrementing the `offset` value will page through only the results that fall within the original constraints (i.e. the last page will contain the last transaction prior to February 1st).  The `totalCount` returned will be the total available resources that match the constraints (in this case, `since` and `until`). As with all other requests, attempting to increase the offset beyond `totalCount` will result in an empty response.


Stream Pagination
-----------------

This pagination uses the `since` and `until` parameters to traverse a constantly growing list of items.  The most important use of this type of pagination is when dealing with historical data from  Telemetry Services.  In this situation, data are constantly being added to the front of the list as vehicles report additional telemetry information.  In order to keep consistent paging, time constraints are placed on the data returned.  In this way a single URL will continue to return the same set of data, even as more data are added to the front of the list.

* `remaining` - the number of items previous to the last item in the returned results and after the `since` parameters
* `limit` - the limit used for the list returned (This will be the limit requested by the client unless one was not passed, in which case the default for this method will be returned, or unless the limit requested by the client was larger than the max allowed for the method, in which case the maximum allowable limit will be returned)
* `links` - an object containing URLs for traversing the pages of the list
  * `prior` - URL for the next (older) page (If the current page is the oldest page, this field will not be returned.)

