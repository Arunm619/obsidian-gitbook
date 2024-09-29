
## Definitions

#### Gradle files

| Kotlin variable | Groovy variable     | Definition                                                                                                                                                                                                                                |
| --------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `minSdk`        | `minSdkVersion`     | The minimum SDK version your app will support, defined in `build.gradle`. For example, if your `minSdk` is 26, this SDK version corresponse to API Level 26 and Android 8, so your app will only run on devices with Android 8 or higher. |
| `targetSdk`     | `targetSdkVersion`  | The SDK version that your app targets, defined in `build.gradle`. This should always be the same as `compileSdk`.                                                                                                                         |
| `compileSdk`    | `compileSdkVersion` | The SDK version that your app compiles against, defined in `build.gradle`. Android Studio uses this SDK version to build your AABs and APKs. This should always be the same as `targetSdk`.                                               |
