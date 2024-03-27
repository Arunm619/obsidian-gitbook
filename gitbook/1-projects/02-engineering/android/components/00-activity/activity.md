
1. **Lifecycle**: An Activity has a lifecycle that is defined by various callback methods. These methods include `onCreate()`, `onStart()`, `onResume()`, `onPause()`, `onStop()`, `onDestroy()`, and `onRestart()`. Each of these methods is called at different stages of the Activity lifecycle, allowing you to perform setup, save state, and clean up as necessary.

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        // Initialize your activity
    }

    override fun onStart() {
        super.onStart()
        // The activity is about to become visible
    }

    override fun onResume() {
        super.onResume()
        // The activity has become visible (it is now "resumed")
    }

    override fun onPause() {
        super.onPause()
        // Another activity is taking focus (this activity is about to be "paused")
    }

    override fun onStop() {
        super.onStop()
        // The activity is no longer visible (it is now "stopped")
    }

    override fun onDestroy() {
        super.onDestroy()
        // The activity is about to be destroyed
    }
}
```

2. **Memory Management**: Android system may kill activities in the background to free up memory. The `onSaveInstanceState()` method is called before the system kills the activity, allowing you to save any state that you'd like to restore later. When the user navigates back to the activity, the `onCreate()` method receives a `Bundle` that contains the state you saved.

```kotlin
override fun onSaveInstanceState(outState: Bundle) {
    super.onSaveInstanceState(outState)
    // Save your activity state here
    outState.putString("MyString", "Welcome back!")
}

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    // Check whether we're recreating a previously destroyed instance
    if (savedInstanceState != null) {
        val myString = savedInstanceState.getString("MyString")
        // Restore your activity state here
    }
}
```

3. **Intents**: Intents are used to start activities and to pass data between them. There are two types of intents: explicit and implicit. Explicit intents specify the activity that should respond to the intent. Implicit intents do not name a specific component, but instead declare a general action to perform.

```kotlin
// Explicit Intent
val intent = Intent(this, SecondActivity::class.java)
intent.putExtra("key", "value")
startActivity(intent)

// Implicit Intent
val intent = Intent(Intent.ACTION_VIEW, Uri.parse("http://www.example.com"))
startActivity(intent)
```

4. **Interaction with other components**: Activities can start other activities, services, or broadcast receivers using intents. They can also interact with content providers to share and store data.

----
