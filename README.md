# PWLocation SDK for Android
================

Version 3.7.8

This is Phunware's Android SDK for the Location module. Visit http://maas.phunware.com/ for more details and to sign up.



Requirements
------------
* Android SDK 4.0.3+ (API level 15) or above
* Architectures supported: armeabi-v7a, arm64-v8a
* Android Support Library 28.0.0


Documentation
-------------

Phunware Location documentation is included both in the Documents folder in the repository as HTML and via maven. You can also find the latest documentation here: http://phunware.github.io/maas-location-android-sdk/


Prerequisites
-------------

Add the following to your `repositories` tag in your top level `build.gradle` file.

 ```XML
 projects {
   repositories {
     ...
     maven {
         url "https://nexus.phunware.com/content/groups/public/"
     }
     ...
   }
 }
 ```

 The location library is broken into separate components so that you can import only the parts of the library needed for your project. All packages can be imported by adding the following to your app's `build.gradle` file
 ```
 implementation 'com.phunware.location:provider-managed:3.7.8'
 implementation 'com.phunware.location:location-core:3.7.8'
 ```
 Importing any of the providers will automatically include the `core` package. When you import `provider-managed`, all associated location provider libraries are included.

Needed Permissions
-----------
In the Android manifest, the following permissions are needed:

```
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
<uses-permission android:name="android.permission.WAKE_LOCK"/>
<uses-feature android:name="android.hardware.bluetooth_le" android:required="false"/>
```

Integration
-----------

#### PwManagedLocationProvider
The PwManagedLocationProvider class allows you to implement Phunware's managed location software to further improve upon locations from your location provider hardware. Currently supported location providers are: CMX, CMX + BLE, BLE, and vBLE (Mist/BeaconPoint). From a code standpoint, setting up a managed location provider is the same regardless of your setup. All of these attributes are set through the MaaS portal for the specific providers that are used. The builder pattern only requires instances of the application, context, and buildingId you are using.

```java
// Create ManagedLocationProviderFactoryBuilder
ManagedProviderFactory.ManagedProviderFactoryBuilder builder =
new ManagedProviderFactory.ManagedProviderFactoryBuilder();

//build location provider
PwManagedLocationProvider provider = builder.application(mApplication)
      .context(mContext)
      .buildingId(<!--YOUR_BUILDING_ID-->)
      .build()
      .createLocationProvider();
```

#### Location Updates
```java
PwLocationListener listener = new PwLocationListener() {
  @Override
  public void onConnectionFailed(PwConnectionResult pwConnectionResult) {
    // handle failure...    
  }

  @Override
  public void onLocationChanged(Location location) {
    // handle update...
  }

  @Override
  public void onStatusChanged(String s, int i, Bundle bundle) {
    // handle status change...
  }

  @Override
  public void onProviderEnabled(String s) {
    // handle provider change...
  }

  @Override
  public void onProviderDisabled(String s) {
    // handle provider change...  
  }
};

locationProvider.requestLocationUpdates(listener);
```

Privacy
-----------
You understand and consent to Phunware’s Privacy Policy located at www.phunware.com/privacy. If your use of Phunware’s software requires a Privacy Policy of your own, you also agree to include the terms of Phunware’s Privacy Policy in your Privacy Policy to your end users.

Terms
-----------
Use of this software requires review and acceptance of our terms and conditions for developer use located at http://www.phunware.com/terms/
