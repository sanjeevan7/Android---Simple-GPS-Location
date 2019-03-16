Layout Design
We will now create the design for the application, first locate the layout file called activity_main.xml, this is the default name when create a new activity. Then write these codes inside your layout file.

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="<a href="http://schemas.android.com/apk/res/android"
" rel="nofollow">http://schemas.android.com/apk/res/android"
</a>    xmlns:app="<a href="http://schemas.android.com/apk/res-auto"
" rel="nofollow">http://schemas.android.com/apk/res-auto"
</a>    xmlns:tools="<a href="http://schemas.android.com/tools"
" rel="nofollow">http://schemas.android.com/tools"
</a>    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.razormist.simplegpslocation.MainActivity">
 
 
 
    <Button
        android:id="@+id/btn_locate"
        android:layout_height="wrap_content"
        android:layout_width="wrap_content"
        android:layout_centerInParent="true"
        android:text="Locate"/>
 
    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Latitude:"
        android:textSize="20sp"
        android:layout_marginRight="100dp"
        android:layout_marginEnd="100dp"
        android:layout_marginBottom="63dp"
        android:layout_above="@+id/btn_locate"
        android:layout_alignRight="@+id/btn_locate"
        android:layout_alignEnd="@+id/btn_locate" />
 
    <TextView
        android:id="@+id/tv_latitude"
        android:textSize="20sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignLeft="@+id/btn_locate"
        android:layout_alignStart="@+id/btn_locate"
        android:layout_alignTop="@+id/textView" />
 
 
    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Longhitud:"
        android:textSize="20sp"
        android:layout_below="@+id/tv_latitude"
        android:layout_alignRight="@+id/textView"
        android:layout_alignEnd="@+id/textView"
        android:layout_marginTop="16dp" />
 
    <TextView
        android:id="@+id/tv_longhitud"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="20sp"
        android:layout_alignBaseline="@+id/textView1"
        android:layout_alignBottom="@+id/textView1"
        android:layout_alignLeft="@+id/tv_latitude"
        android:layout_alignStart="@+id/tv_latitude" />
 
 
</RelativeLayout>
Android Manifest File
The Android Manifest file provides essential information about your app to the Android system in which the system must required before running the code. It describe the overall information about the application. It contains some libraries that needed to access the several method within the app.

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="<a href="http://schemas.android.com/apk/res/android"
" rel="nofollow">http://schemas.android.com/apk/res/android"
</a>    package="com.razormist.simplegpslocation">
 
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
 
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity"
            android:configChanges="orientation"
            android:screenOrientation="portrait">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
 
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
Creating the GPS Locator
This code contains the script for the GPS. This code will access the device GPS to get the information about the actual location of the device. To do that create a new java class called GPSLocator then write these block of codes inside of it.

package com.razormist.simplegpslocation;
 
import android.Manifest;
import android.content.Context;
import android.content.pm.PackageManager;
import android.location.Location;
import android.location.LocationListener;
import android.location.LocationManager;
import android.os.Bundle;
import android.support.v4.content.ContextCompat;
import android.widget.Toast;
 
/**
 * Created by Arvin on 4/5/2018.
 */
 
public class GPSLocator implements LocationListener {
    Context context;
 
    public GPSLocator(Context c){
        context = c;
    }
 
    public Location GetLocation(){
        if(ContextCompat.checkSelfPermission(context, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED){
            Toast.makeText(context, "Permission not granted", Toast.LENGTH_SHORT).show();
            return  null;
        }
 
        LocationManager locationManager = (LocationManager) context.getSystemService(Context.LOCATION_SERVICE);
        boolean isGPSEnabled = locationManager.isProviderEnabled(LocationManager.GPS_PROVIDER);
        if(isGPSEnabled){
            locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 6000, 10, this);
            Location location = locationManager.getLastKnownLocation(LocationManager.GPS_PROVIDER);
            return location;
        }else{
            Toast.makeText(context, "No GPS Detected", Toast.LENGTH_SHORT).show();
        }
 
        return null;
    }
 
    @Override
    public void onLocationChanged(Location location) {
 
    }
 
    @Override
    public void onStatusChanged(String provider, int status, Bundle extras) {
 
    }
 
    @Override
    public void onProviderEnabled(String provider) {
 
    }
 
    @Override
    public void onProviderDisabled(String provider) {
 
    }
 
 
}
The Main Function
This code contains the main function of the application. This code will start gathering the data that has been locate through the device GPS and display the result when the button is clicked. To start with first locate your MainActivity java file and open it, then write these variable inside the MainActivity class.

Button btn_locate;
TextView tv_latitude, tv_longhitud;
Finally, initialize the require methods inside the onCreate method to run the application.

  btn_locate = (Button)findViewById(R.id.btn_locate);
        tv_latitude = (TextView)findViewById(R.id.tv_latitude);
        tv_longhitud = (TextView)findViewById(R.id.tv_longhitud);
 
        ActivityCompat.requestPermissions(MainActivity.this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, 123);
        btn_locate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                GPSLocator gpsLocator = new GPSLocator(getApplicationContext());
                Location location = gpsLocator.GetLocation();
                if(location != null){
                    double latitude = location.getLatitude();
                    double longhitud = location.getLongitude();
                    tv_latitude.setText(String.valueOf(latitude));
                    tv_longhitud.setText(String.valueOf(longhitud));
                }
            }
        });
Try to run the app and see if it worked.

There you have it we have created a Simple GPS Location using Android. I hope that this tutorial help you to what you are looking for. For more updates and tutorials just kindly visit this site. Enjoy Coding!!!
