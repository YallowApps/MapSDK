# Yallow MapSDK Tracking for android

## Introduction 
this documentation is describe how to connect your android application with Yallow map sdk tracking. this library provide map view with full tracking of your order, you can use it as a view and customize it as you want. 
first you should have an `api key` provided from Yellow company **if you don't have one please contact with our sales team on this website https://www.yallow.com/contact.**


## Gradle setup
### in your  project gradle add this:
```

allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://dl.bintray.com/yallow/YallowMapSDK/" } // and this line
    }
}
```

### in your app gradle please add this code: 

```

dependencies {  
     // your own dependencies
    implementation 'com.yallow:YallowMapSDK:0.0.39'

   
}
```
now your gradle is ready.

## Application setup:
in your application class add these line of code if you don't have an application class add it in your first activity 

```

class YourApplication : Application(){
    val API_KEY = "YOUR_API_KEY"

    override fun onCreate() {
        super.onCreate()
        // your code
        MapSDK.init(this,API_KEY,object : YallowMapSDKListener{
            override fun onInitFail(message: String) {
              // you can show error in message
            }

            override fun onInitSuccessfully() {
                // make sure that everything is working
            }
        })
    }
}


```

## Map design
this map view is inherited from google map view so you can customize it as you want 
```
  <com.yallow.yallowmapsdk.views.YallowMapView
        android:id="@+id/trakingMap"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:driverMarkerImage="@drawable/driverImage"
        app:pickUpMarkerImage="@drawable/abc_vector_test"
        app:customerMarkerImage="@drawable/abc_vector_test"
        />
        
   ```
   
 the sdk prvoid full customization on the markers (pickup, driver and customer) so you can add it through xml or in the kotlin/java code
 
 
 
 ## Tracking activity
 in the `onCreate()`  your tracking activity add this code
   ```
override fun onCreate(savedInstanceState: Bundle?) {
      //... your code

        trakingMap.initMap(savedInstanceState)
        trakingMap.orderId = ORDER_ID_THAT_YOU_WANT_TO_TRACK
        trakingMap.trackingDetailsListener = this

    }
  
  ```

the interface should provide three functions which are : 
```
   override fun onDriverLocationUpdate(latLng: LatLng) {
        // prvoide the driver location each time updated
    }
    
    override fun onOrderUpdate(order: Order) {
      // provide order update each time updated 
    }
    override fun onOrderFail(message: String) {
       // show any error message that return from server       
    }
    
 ```
      
 you also need to `ovrride` the activity states and connect it to the mapView:
 ```
  override fun onStart() {
        super.onStart()
        trakingMap!!.onStart()
    }

    override fun onResume() {
        super.onResume()
        trakingMap!!.onResume()
    }

    override fun onPause() {
        super.onPause()
        trakingMap!!.onPause()
    }

    override fun onStop() {
        super.onStop()
        trakingMap!!.onStop()
    }

    override fun onLowMemory() {
        super.onLowMemory()
        trakingMap!!.onLowMemory()
    }

    override fun onDestroy() {
        super.onDestroy()
        trakingMap!!.onDestroy()
    }
```
you can read markers from web using this line of code:
```
trakingMap.usingMarkerFromUrl(true)

```




