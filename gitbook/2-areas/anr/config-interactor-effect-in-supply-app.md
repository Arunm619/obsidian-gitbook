
Supply App has an instance of Config Interactor injected into it. 
But that is unused in the app layer. 

Config Interactor present in the Application class. [Source](https://github.com/Meesho/supply_android/blob/31e0797d289083aacf8078c68bdd6fad91e82f5e/app/src/main/java/com/meesho/supply/main/SupplyApplication.kt#L55)


Logs for when the app was cold started multiple times when the config interactor was created.

```
---------------------------- PROCESS ENDED (10195) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (11796) for package com.meesho.supply.debug ----------------------------
19:53:06.874  D  Arun, init started - ConfigInteractor 1710598986874 ms
19:53:06.882  D  Arun, got ready at 8 ms
---------------------------- PROCESS ENDED (11796) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (12175) for package com.meesho.supply.debug ----------------------------
19:53:21.201  D  Arun, init started - ConfigInteractor 1710599001201 ms
19:53:21.214  D  Arun, got ready at 13 ms
---------------------------- PROCESS ENDED (12175) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (12555) for package com.meesho.supply.debug ----------------------------
19:53:31.317  D  Arun, init started - ConfigInteractor 1710599011317 ms
19:53:31.325  D  Arun, got ready at 8 ms
---------------------------- PROCESS ENDED (12555) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (12913) for package com.meesho.supply.debug ----------------------------
19:53:40.769  D  Arun, init started - ConfigInteractor 1710599020769 ms
19:53:40.790  D  Arun, got ready at 21 ms
---------------------------- PROCESS ENDED (12913) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (13273) for package com.meesho.supply.debug ----------------------------
19:53:50.677  D  Arun, init started - ConfigInteractor 1710599030677 ms
19:53:50.687  D  Arun, got ready at 10 ms
---------------------------- PROCESS ENDED (13273) for package com.meesho.supply.debug ----------------------------

---------------------------- PROCESS STARTED (13273) for package com.meesho.supply.debug ----------------------------
19:53:50.677  D  Arun, init started - ConfigInteractor 1710599030677 ms
19:53:50.687  D  Arun, got ready at 10 ms
---------------------------- PROCESS ENDED (13273) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (13763) for package com.meesho.supply.debug ----------------------------
19:59:12.942  D  Arun, init started - ConfigInteractor 1710599352942 ms
19:59:12.955  D  Arun, got ready at 13 ms
---------------------------- PROCESS ENDED (13763) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (14180) for package com.meesho.supply.debug ----------------------------
19:59:21.344  D  Arun, init started - ConfigInteractor 1710599361343 ms
19:59:21.352  D  Arun, got ready at 9 ms
---------------------------- PROCESS ENDED (14180) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (14563) for package com.meesho.supply.debug ----------------------------
19:59:30.266  D  Arun, init started - ConfigInteractor 1710599370265 ms
19:59:30.274  D  Arun, got ready at 8 ms
---------------------------- PROCESS ENDED (14563) for package com.meesho.supply.debug ----------------------------
---------------------------- PROCESS STARTED (14929) for package com.meesho.supply.debug ----------------------------
19:59:42.271  D  Arun, init started - ConfigInteractor 1710599382270 ms
19:59:42.278  D  Arun, got ready at 8 ms

```


Test device - One plus 7 
Test OS - Android 13
Total Iterations = 10
Sum of iterations = 8 + 13  + 8 + 21 + 10 + 13 + 9 + 8 + 8 = 98 ms
Mean = 9.8 ms 



