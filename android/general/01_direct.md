Direct SDK
==========

The first step to access Vinli Devices is to discover available Vinli Devices in the area.


    Observer<Device> devices = VinliDevices.createDeviceObservable(activity);


Calling `VinliDevices#createDeviceObservable` returns an `Observer` of devices that will report available devices as they are discovered.

Once a device is obtained, the developer needs to create a `DeviceInterface` by calling `Device#createDeviceInterface` with their current Android context.

To obtain relatively static information such as VIN, device ID, and DTC codes, the device interface exposes `Device#readVin`, `Device#readChipId`, and `Device#readDtcCodes`, respectively

Frequently updated information is accessed by supplying the `Pid` (for Parameter IDs) constant corresponding to the desired vehicle data. To observe realtime changes to the data, pass the desired `Pid` to `DeviceInterface#observe`. To synchronously retrieve the latest value for a parameter, pass the desired `Pid` to `DeviceInterface#getLatest`. Examples of available `Pid` constants include `Pid.Rpm` and `Pid.Speed_Mph`

* To observe realtime streams of frequently updated device characteristic, the device interface provides `Device#observe{{characteristic}}` methods for each available charateristic, e.g. `Device#observeRpm` and `Device#observeSpeedMph`
* To synchronously get only the latest observed value raw OBD value for a characteristic, the device interface exposes a `Device#getLatest{{characteristic}}` method for each available characteristic, e.g. `Device#getLatestRpm` and `Device#getLatestSpeed`

Example Android fragment to show a device's vehicle's VIN, RPM, and speed:


    public class DeviceDetailFragment extends Fragment {
        public static final String DEVICE = "vinli_device";

        private final List<Subscription> mCreatedSubscriptions = new ArrayList<Subscription>();
        private final List<Subscription> mVisibleSubscriptions = new ArrayList<Subscription>();

        private Device mDevice;
        private DeviceInterface mDi;

        @Override public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            if (getArguments().containsKey(ARG_ITEM_ID)) {
                mDevice = getArguments().getParcelable(ARG_ITEM_ID);
                mDi = mDevice.createDeviceInterface(getActivity());
            } else {
              throw new IllegalArgumentException("missing device");
            }
        }

        @Override public View onCreateView(LayoutInflater inflater, ViewGroup
                container, Bundle savedInstanceState) {
            final View rootView = inflater.inflate(R.layout.fragment_device_detail, container, false);

            ((TextView) rootView.findViewById(R.id.name)).setText(mDevice.getName());

            final TextView vin = (TextView) rootView.findViewById(R.id.vin);
            mCreatedSubscriptions.add(AndroidObservable.bindFragment(this, mDi.readVin())
              .subscribe(new Observer<String>() {
                  @Override public void onCompleted() {}
                  @Override public void onError(Throwable e) {
                      vin.setText("failed to fetch vin");
                  }
                  @Override public void onNext(String s) {
                      vin.setText("VIN: " + s);
                  }
                }));

            return rootView;
        }

        @Override public void onResume() {
            super.onResume();

            final TextView rpm = (TextView) getView().findViewById(R.id.rpm);
            mVisibleSubscriptions.add(AndroidObservable.bindFragment(this, mDi.observe(Pid.Rpm))
               .subscribe(new Observer<Float>() {
                   @Override public void onCompleted() {}
                   @Override public void onError(Throwable e) {
                       rpm.setText("failed to get rpm");
                   }
                   @Override public void onNext(Float f) {
                       rpm.setText("rpm: " + f);
                   }
               }));

            final TextView speedMph = (TextView) getView().findViewById(R.id.speed_mph);
            mVisibleSubscriptions.add(AndroidObservable.bindFragment(this, mDi.observe(Pid.Speed_Mph))
               .subscribe(new Observer<Integer>() {
                   @Override public void onCompleted() {}
                   @Override public void onError(Throwable e) {
                       speedMph.setText("failed to get speed Mph");
                   }
                   @Override public void onNext(Integer i) {
                       speedMph.setText("speed Mph: " + i);
                   }
               }));
        }

        @Override public void onPause() {
            super.onPause();
            unsubscribe(mVisibleSubscriptions);
        }

        @Override public void onDestroyView () {
            super.onDestroyView();
            unsubscribe(mCreatedSubscriptions);
        }

        private static void unsubscribe(List<Subscription> subs) {
            for (Subscription s : subs) {
              s.unsubscribe();
            }
            subs.clear();
        }
    }
