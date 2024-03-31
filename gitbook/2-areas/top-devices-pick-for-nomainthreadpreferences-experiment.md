
### fsync issue - [Google Play Console](https://play.google.com/console/u/0/developers/8586507075174719506/app/4974541337588252131/vitals/crashes/d7e9dc507f798ad5f6bed85136981a4b/details?isUserPerceived=true&days=28)

**Top Devices:**
1. realme RMX2185 
2. OPPO OP4BFB
3. xiaomi jasmine_sprout
4. vivo 1907
5. realme RMX3063
6. vivo 1915
7. realme RMX1911

![[devices-anr-fsync.png]]

----


### art::ConditionVariable::WaitHoldingLocks(art::Thread*) - [Google Play Console](https://play.google.com/console/u/0/developers/8586507075174719506/app/4974541337588252131/vitals/crashes/0080080aac558d72f1afb4ea3fec9dd5/details?isUserPerceived=true&days=28)


**Top Devices**

1. realme RMX2185
2. xiaomi jasmine_sprout
3. realme RMX3063
4. realme RMX1911
5. OPPO OP4F2F
6. Nokia PL2_sprout
7. Realme RMX1825


![[devices-anr-hold-lock.png]]


---

**Union of the devices selected so far**
1. realme RMX2185 
2. OPPO OP4BFB ( found on MP - CPH2083 - Oppo A12 - Android 9.0)
3. xiaomi jasmine_sprout (Found on mixpanel its called Mi A2)
4. vivo 1907
5. realme RMX3063
6. vivo 1915
7. realme RMX1911
9. OPPO OP4F2F
10. Nokia PL2_sprout
11. Realme RMX1825



---
**Final List For Experiment**


| Model Name | Device Name    |
| ---------- | -------------- |
| RMX2185    | Realme C11     |
| vivo 1907  |                |
| RMX3063    | Realme C20     |
| vivo 1915  |                |
| RMX1911    | Realme 5       |
| Mi A2      | jasmine_sprout |
| CPH2083    | Oppo A12       |


We will be enabling the experiment today and we will keep a watch on the shared pref ANR issues mentioned above for their shift in trend. Post that, we will be concluding on what is the next steps.


--- 
Creating an audience 



Query for getting the audience id 
```sql
select id from  
(select distinct user_id as id  
from silver.mixpanel_android__app_open  
where date(year||'-'||month||'-'||day) >= (current_date - interval '60' day) and model in ('RMX2185', 'vivo 1907','RMX3063','vivo 1915','RMX1911','Mi A2','CPH2083')  
and app_build_number >= 500)
```


Audience ID is `114543`
Experiment number is `612`
[Supply Admin Panel](https://admin.meeshosupply.com/ab-experiment/612)

CON-360


App build number is chosen as **500**. 
![[500-app-version-split.png]]