

App Startup 
1. Process init (this is purely android os)
2. Content Provider init 
3. App subclass init
4. Launch activity init

Amazon has stated that every 100ms of latency costs them 1% of revenue in sales. It goes without saying that there is a strong incentive to improve startup time for their business.

User like fast experiences more likely to be engaged for longer 
App store metrics - One of the core vital metrics - App store ranking 


<5s   - Cold startup duration
<2s   - Warm startup duration
<1.5s - Hot startup duration

Deferral Patterns

Doing work where it needs to be done. 
Not before or not after 

Procastinating with Lazy 
Lazy delegation in Kotlin `by lazy`
Eg. Shared Preferences 


Lazy in Dagger
`dagger.Lazy`


Deferral with Dynamic Feature Module 

Create new dynamic modules 

```groovy
android {
dynamicFeatures = ['dynamicmaps:']
// implementation(project(":feature:maps"))
}
```

Now this will be installed post app startup post installation


Update the dynamic map module config 

```groovy
plugins {
id("com.android.dynamic-feature")
android {
//...
}
dependenceis {
implementation(project(":app"))
implementation(project(":feature:maps"))
}
//...
}
```

Runtime installation 

```kotlin
val splitInstallManager = SplitIntallManagerFactory.create(this)
val request = SplitInstallRequest
	.newBuilder()
	.addModule("dynamicmaps")
	.build()
splitInstallManager
	.startInstall(request)
	.addOnSuccessListener { sessionId -> 
		//...
	}
	.addOnFailureListener { exception -> 
		//...
	}
```


for installing a module all it takes is just above code.


background ANRs 
Ads Library - caused due to pre-caching ads - creating webviews on main thread.
Not good in app startup. Defer it.

### Parallel Performance Patterns

use coroutines to initialise sp in init block but immediately accessing it will cause lateinit exception

Solution 1 :
![[Screenshot 2024-11-25 at 4.10.40 AM.png]]

![[Screenshot 2024-11-25 at 4.10.58 AM.png]]

Solution 2 :

![[Screenshot 2024-11-25 at 4.11.06 AM.png]]![[Screenshot 2024-11-25 at 4.11.19 AM.png]]

How it works ?

green - main 
yellow - bg thread

![[Screenshot 2024-11-25 at 4.12.14 AM.png]]


### Divide and Conquer 

Logger  
Admob
okHttp 
RoomDb 
Google Maps


Logger  (100ms)
Admob (500ms)
okHttp  (100ms)
RoomDb  (400ms)
Google Maps (500ms)

Total duration is ~1600ms

We can do better
![[Screenshot 2024-11-25 at 4.14.07 AM.png]]


**Advanced Parallelization**

![[Screenshot 2024-11-25 at 4.16.22 AM.png]]
![[Screenshot 2024-11-25 at 4.16.09 AM.png]]![[Screenshot 2024-11-25 at 4.17.52 AM.png]]


#### Jetpack App Startup Lib

- Introduces basic init component
- can intelligently orders init based on dependencies

![[Screenshot 2024-11-25 at 4.18.52 AM.png]]


Deferring Content Providers 

1. Remove the content provider declaration from the merged manifest. 
2. Create a new initializer to replace the content provider 
3. In the new initializer, follow the same initialization code as the content provider
4. Initialize the new Initializer in your startup flow 
5. (optional) initialize the initializer asynchronously



Closing thoughts 

App Performance programming requires lots of tools to tackle perf challenges. Knowing them and having the wisdom to use them appropriately is crucial. 

