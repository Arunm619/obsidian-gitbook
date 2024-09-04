

Multi supplier cart is a major update to our app where the users got the ability to add multiple products from various suppliers all in one order. 


App version for MSC is **403**.

So Pre-MSC app version code is **< 403**.


Details on orders with these app versions :
To be filled.

NMV/MAU: 
Order Count: 


----

This is the current force update details we are sending in config. 

"force_update": {  
    "title": "New & Improved Features One Click Away",  
    "message": "Update Your Meesho App & Get ₹10 Credits",  
    "min_version_code": 189  
  }

```kotlin
private fun needsForceUpdate(forceUpdate: ForceUpdate?): Boolean {  
    if (forceUpdate == null) return false  
    val minVersionCode = forceUpdate.minVersionCode  
    return minVersionCode != null && BuildConfig.VERSION_CODE < minVersionCode  
}
```


We need to update this to **403**

---
