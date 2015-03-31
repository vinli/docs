Net SDK
========

The Vinli Net SDK provides access to all of the same Vinli backend services as provided by the web API. The benefit of using the Vinli Net SDK is that we will provide all of the networking, authentication, parsing, and pagination, helping to make Vinli Android app development even easier.

The primary interface provided by the Vinli Net SDK is the `VinliApp`. `VinliApp` instances are created using the developer's app ID and secret.

For requests that return non-paginated content, an `Observable<ContentType>` is returned.


    private final VinliApp app = VinliApp.create("appId", "appSecret");
    app.diagnoseDtcCode("P0300").subscribe(new Observer<Dtc>() {
        @Override public void onCompleted() {}
        @Override public void onError(Throwable e) {
            Log.e("DtcCodesObservable", "failed to fetch DTC Code", e);
        }

        @Override public void onNext(Dtc dtc) {
            Log.d("DtcCodesObservable", "got DTC Code: " + dtc);
        }
    });


For requests that return paginated content, an `Observable<Page<ContentType>>` is returned. Each `Page<ContentType>` provides access to the content of the page as well as the ability to load the next and previous pages. To make displaying Android `ListView`s of paginated content easier, the Vinli Net SDK provides the utility `PageAdapter<ContentType>` class. To load all of a user's devices:


    private final VinliApp app = VinliApp.create("appId", "appSecret");
    final PageAdapter<li.vin.net.Device> adapter = new DeviceAdapter(activity);
    AndroidObservable.bindFragment(this, app.getDevices()).subscribe(adapter);

