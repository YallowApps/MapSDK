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
    implementation 'com.yallow:YallowMapSDK:0.0.28'

   
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
        MapSDK.init(this,API_KEY)
    }
}


```

## Map design
this map view is inherited from google map view so you can customize it as you want 
```
  <com.yallow.yallowmapsdk.views.YallowMapView
        android:id="@+id/map"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        />
        
   ```
