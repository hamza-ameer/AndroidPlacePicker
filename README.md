# AndroidPlacePicker
Implement Placepicker in android Cracked



1)

Update your App Level Gradle file with following dependency:


    dependencies {
       implementation 'com.google.android.gms:play-services-places:16.1.0'
    }


2)

Add the following permissions in your menifest file:
  
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.INTERNET" />


3)

Update your activity_main.xml file with the following TextView and Button:

  
    <TextView
        android:id="@+id/MyLocation"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.323"></TextView>

    <Button
        android:id="@+id/BtnPickLocation"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#000"
        android:text="Pick Location"
        android:textColor="#fff"
        android:layout_margin="20dp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.604"></Button>


4)

Update your MainActivity.java file with the following code:

		Button btn_PickLocation;
		TextView tv_MyLocation;
		WifiManager wifiManager;
		private final static int PLACE_PICKER_REQUEST = 999;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btn_PickLocation=(Button)findViewById(R.id.BtnPickLocation);
        tv_MyLocation=(TextView) findViewById(R.id.MyLocation);
        wifiManager= (WifiManager) this.getApplicationContext().getSystemService(Context.WIFI_SERVICE);

        btn_PickLocation.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

		//Disable Wifi
                wifiManager.setWifiEnabled(false);
                openPlacePicker();
            }
        });
    }

     private void openPlacePicker() {
        PlacePicker.IntentBuilder builder = new PlacePicker.IntentBuilder();
        try {
            startActivityForResult(builder.build(this), PLACE_PICKER_REQUEST);

	    //Enable Wifi
            wifiManager.setWifiEnabled(true);

        } catch (GooglePlayServicesRepairableException e) {
            Log.d("Exception",e.getMessage());

            e.printStackTrace();
        } catch (GooglePlayServicesNotAvailableException e) {
            Log.d("Exception",e.getMessage());

            e.printStackTrace();
        }

    }


     @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (resultCode == RESULT_OK) {
            switch (requestCode){
                case PLACE_PICKER_REQUEST:
                    Place place = PlacePicker.getPlace(MainActivity.this, data);

                    double latitude = place.getLatLng().latitude;
                    double longitude = place.getLatLng().longitude;
                    String PlaceLatLng = String.valueOf(latitude)+" , "+String.valueOf(longitude);
                    tv_MyLocation.setText(PlaceLatLng);

            }
        }
    }



5) 
 
 		Test Your PlacePicker and Enjoy :)


