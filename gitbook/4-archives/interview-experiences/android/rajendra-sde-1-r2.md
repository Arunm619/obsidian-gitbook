Worked on lot of live ola features (fancy stuff with )
bound services
BT 

--
Personal
- Sincere - came 5 mins before interview
- Came to the terrace to attend the interview because of power cut
- Android experience - 1.9 years (July 2022)
- QR code attendance system.


Android

project: 
5 mins for reading - done
Understanding of requirements - done
Clarifying approach - not done

coroutines : define a job + 
networking i/o dispatcher
general coroutines - lifecycle scope  (viewmodel scope)

Started thinking about all reqs and stuck with parallelism
suggested one by one:
1. first requirement : implemented without error handling. Fixed it after pinpointing.
Facing Class not found exception when trying to run the project.
Fixed it and got stuck. Couldn't come up with solution. 



Red flags:
- Instead of coroutine context he sent application context in the coroutine scope.
- Creates global object for job - fixed this after asking. 
- Too much googling
- Couldn't run anything.



Architecture at ola - sub module architecture  - multi module
- own git sub modules


- can we run on network api calls on main thread?
	- ANR - Main thread
	- I/O thread

MCQ:
1. Main method - correct
2. Dispatchers - correct
3. View model destruction - wrong 
4. Live data usage correct
5. Singleton - correct
6. device configuration - data persistence - viewmodel - correct
7. Shared preferences - wrong
8. Lifecycle of Activity being first visible - correct
9. Linear layout for stacking - wrong
10. Network call main thread  - correct
11. long running continued processing - correct


-----


**Projects***

Most challenging project 

- proximity locking and unlocking 
- native code
- ds model 
- BT RSI 
- distance between device and scooter 
- RSI value strength
- Accelerometer - RSI - light sensor
- Imaginary circle 
- JNI - cpp code

worked with data science team
Can you tell me about JNI
Java interface in cpp implementation.
ds model running on cpp.

tensor flow library 
JNI was not used. 
Tensor flow lite is used. 
Heavy model - more inference time - more memory
App size - heavy 


Bound services 
Fg, bg services
AIDL - Interface 
One app to another app comm. 

Service based architecture 

HMI - Main service
Proxy Service 
Auto turn off indicator 


---

Articulation of thoughts was okay. Struggling a bit.
