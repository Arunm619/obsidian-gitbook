Android Run Time

## **ART**

With a newer android version specifically from 4.4 version KitKat, there is the concept of ART as an alternative to DVM. ART(Android Run Time) is a successor of DVM which uses the same bytecode and .dex files (but not .odex files), with the succession aiming at performance improvements transparent to the end-users.  Android 5.0 “Lollipop” is the first version in which ART is the _only_ included runtime. Now the thing that ART does is bring apps that are fully compiled when they’re installed on the device. Therefore, higher performance as no need to convert code to bytecode then compile. But the downside is you need more storage space and a little longer to install because of compilation during installation meaning it has to live on the device all the time. Hence, instead of relatively small java code, we have larger bytecode/machine code. You may have heard the terms **odexed** and **de-odexed**. What is done in this instance is you take a small part of the application and then precompile it they can go ahead and make a portion of their application optimized to run on their device, and so they’ve now precompiled that section of the app and the rest of its compiled at runtime. So this makes it just a little faster and more performant than in Dalvik. But this approach takes a little more storage space.


|DALVIK VIRTUAL MACHINE|ANDROID RUN TIME|
|---|---|
|Faster Booting time|Rebooting is significantly longer|
|Cache builds up overtime|The cache is built during the first boot|
|Occupies less space due to JIT|Consumes a lot of storage space internally due to AOT|
|Works best for small storage devices|Works best for Large storage devices|
|Stable and tested virtual machine|Experimental and new – not much app support comparatively|
|Longer app loading time|Extremely Faster and smoother Faster and app loading time and lower processor usage|
|Uses JIT compiler(JIT: Just-In-Time)  <br>Thereby resulting in lower storage space consumption|Uses AOT compiler(Ahead-Of-Time) thereby compiling apps when installed|
|Application lagging due to garbage collector pauses and JIT|Reduced application lagging and better user experience|
|App installation time is comparatively lower as the compilation is performed later|App installation time is longer as compilation is done during installation|
|DVM converts bytecode every time you launch a specific app.|ART converts it just once at the time of app installation. That makes CPU execution easier. <br><br>Improved battery life due to faster execution.|
|It is slower than ART.|It is faster.|
|It does not provide optimized battery life as it consumes more power.|It provides optimized battery performance as it consumes less power.|
|While considering Booting, then this device is fast.|It lags in term of booting.|

----

----

**DVM** 
The **Dalvik Virtual Machine (DVM)** is an android virtual machine optimized for mobile devices. It optimizes the virtual machine for _memory_, _battery life_ and performance

The Dex compiler converts the class files into the .dex file that run on the Dalvik VM. Multiple class files are converted into one dex file.
