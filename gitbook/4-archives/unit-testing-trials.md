
Created a sample project with unit tests.

**4 classes** 

- ExampleUt1
- ExampleUt2
- ExampleUt3
- ExampleUt4

Each class has 5 methods. 
Each tests does an addition with one second sleep. 
Therefore the total time taken would be  
	= 4 * 5
	= 20
	= 20 test cases * 1 second per test
	= **20 seconds**. 


----
Below command confirms that:

`./gradlew testDebugUnitTest --rerun-tasks` 
+2 seconds overhead for other gradle stuff. 

```
BUILD SUCCESSFUL in 22s
22 actionable tasks: 22 executed
```

**--rerun-tasks option:**

- Forces Gradle to ignore up-to-date checks for tasks.
- Reruns specified tasks even if inputs and outputs haven't changed.
- Useful during development/testing to ensure tasks are always executed.

----
maxparallelforks worked. 

----

Sharding the unit tests based on categories help reduce time 
To represent the categories or label tests, we need to create marker interfaces. This simple interfaces will be will use to classify our tests and run them in parallel.

```kotlin
interface RobolectricTests

interface UnitTests

interface FastTests

interface SlowTests
```

> Note: JUnit categories can take any class name as a category, it is not required to create custom interfaces. We can use any predefine classes as well to categorize tests.

