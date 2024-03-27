
- Occasionally android system can kill our app - its called process death
- Terminate App button in studio can simulate process death
- State loss happens which leads to weird states when app is resumed from recent tasks list
- User resumes the screen they minimised at (eg. Payment page)
-  [SavedStateHandle  |  Android Developers](https://developer.android.com/reference/androidx/lifecycle/SavedStateHandle) to resuce
- This is a key-value map that will let you write and retrieve objects to and from the saved state. These values will persist after the process is killed by the system and remain available via the same object.
