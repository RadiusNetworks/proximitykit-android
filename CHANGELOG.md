Version 0.7.0 - July 30, 2015
-----------------------------

Enhancements:

- Add `ProximityKitManager#setPartnerIdentifier(String)` and
  `ProximityKitManager#clearPartnerIdentifier()` to the public API. Allowing
  the configuration of an additional custom identifier which is attached to
  analytic events.


Version 0.6.3 - July 30, 2015
-----------------------------

Bug Fixes:

- Move calls to Status Kit analytics into a custom serial background queue;
  thus no longer consuming resources from `AsyncTask`'s thread pools
- Update to [AltBeacon/android-beacon-library](https://github.com/AltBeacon/android-beacon-library)
  version [2.3.5](https://github.com/AltBeacon/android-beacon-library/releases/tag/2.3.5)
- Fix edge case on spotty, slow, or no networks which causes every ranged
  beacon event to attempt a status update over the network.


Version 0.6.2 - May 28, 2015
----------------------------

Bug Fixes:

- Fix issue with ranging where the ranging timestamp is incorrectly store as a
  future time due to background task execution delays
- Fix issue where a group of beacons are ranged at the same time but may report
  slightly different timestamps


Version 0.6.1 - May 5, 2015
---------------------------

Bug Fixes:

- Fix timestamp parsing and formatting bug which can occur when Director is
  called from multiple threads.


Version 0.6.0 - April 28, 2015
------------------------------

Enhancements:

- Support for [Director](https://director.radiusnetworks.com) analytics.


Version 0.5.0 - April 10, 2015
------------------------------

Enhancements:

- Add support for explicit region monitoring and ranging.

  Previous functionality can be achieved by not checking "Explicit Region
  Monitoring" on the kit's "Properties -> Settings" page on the server. In
  order to control which regions are ranged and monitored ensure this option is
  checked.

  On the server, regions have an "Advanced Settings" option where you can check
  "Enable Ranging" and/or "Enable Region Monitoring".

Deprecations:

- The `ProximityKitManager#getMaxRegionsBeforeRollup` and
  `ProximityKitManager#setMaxRegionsBeforeRollup` methods are now no-ops. Use
  the new explicit region monitoring behavior instead.
- The `KitBeacon#to_region` conversion method was never intended to be
  `public`. To convert a `KitBeacon` to a `Region` construct a new region using
  the identifiers from the beacon.


Version 0.4.0 - March 16, 2015
------------------------------

Enhancements:

- Add support for version 6.1 and 6.5 of the Google Play Services Library.

Bug Fixes:

- Update to [AltBeacon/android-beacon-library](https://github.com/AltBeacon/android-beacon-library)
  version [2.1.4](https://github.com/AltBeacon/android-beacon-library/releases/tag/2.1.4)


Version 0.3.1 - March 11, 2015
------------------------------

Bug Fixes:

- Remove static compiled 'support-v4' library.


Version 0.3.0 - February 20, 2015
---------------------------------

Enhancements:

- Add ability to set a threshold on how many regions can be registered before
  being automatically combined. This allows for large region sets but keeps the
  device from getting overwhelmed.

Bug Fixes:

- Fix `NullPointerException` which occurs when requesting a Kit's overlays when
  it does not have a map.  (RadiusNetworks/proximitykit-android/#2)
- Fix bug preventing geofencing from working with API levels below 18.
  Geofences rely on Google Play services so they still require a min Android
  API level of 9.
- Reduce the `minSdkVersion` to 4; this is the lowest function API level which
  Proximity Kit will work with.
- Update to [AltBeacon/android-beacon-library](https://github.com/AltBeacon/android-beacon-library)
  version [2.1.3](https://github.com/AltBeacon/android-beacon-library/releases/tag/2.1.3)
- Prevent services from being exported system wide.


Version 0.2.0 - October 27, 2014
--------------------------------

Enhancements:

- Add `ProximityKitManager#stop()` to the public API

  This stops any further syncing with the cloud. It additionally, unregisters
  any beacons and geofences which are being monitored.
- Attempts to auto update database of Android model specific distance
  calculations
- Added generation of beacon bytearrays from BeaconParser in support of future
  transmitter on release of Android


Version 0.1.1 - October 23, 2014
--------------------------------

Bug Fixes:

- Fix erroneous warning when geofence action queue has been emptied and a new
  action is added. This fix also causes the new action to start running.
- Fix race condition reporting erroneous warning caused by multi-step actions
  are rapidly added to the queue.
- Fix `ClassCastException` caused if the AltBeacon `BeaconManager` is created
  prior to the Proximity Kit manager being instantiated.
- Uses distance calculations specific to the Android model
- Fix bug with RegionBootstrap setting background mode incorrectly on app
  launch


Version 0.1.0 - September 4, 2014
---------------------------------

- Requires JDK 1.7+
- Requires Android minimum SDK version 9+
- [AltBeacon.org](http://altbeacon.org/) support for monitoring beacon regions
  using the v1.0 specification
- Uses [AltBeacon/android-beacon-library](https://github.com/AltBeacon/android-beacon-library)
  version [2.0-beta6](https://github.com/AltBeacon/android-beacon-library/releases/tag/2.0-beta.6)
- Geofence support using [Google Play
  services](https://developer.android.com/google/play-services) 4.4+

Major technical focuses for this release were on adding geofence and AltBeacon
v1.0 spec support. Receiving notification of various events is provided by
registering as one or more a callbacks. These callbacks are defined by several
interfaces based on the activity and type of region.

- `ProximityKitMonitorNotifier`

  Notifies the app when the host device has come with-in or moved out-of
  proximity with any of the registered beacons.

- `ProximityKitRangeNotifier`

  Available while the host device is with-in a registered beacon regions.
  Provides the app with constant notifications about the device's relative
  proximity to those regions.

- `ProximityKitGeofenceNotifier`

  Notifies the app when the host device has come with-in or moved out-of
  any of the registered geofence regions.

- `ProximityKitSyncNotifier`

  Notifies the app after Proximity Kit has been synced with the cloud.
