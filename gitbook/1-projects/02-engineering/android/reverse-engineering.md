 

[DroidKaigi 2022 - The art of hiding sensitive info in plain sight | George Kortsaridis [EN] - YouTube](https://www.youtube.com/watch?v=FOM1P3ivm0s&ab_channel=DroidKaigi)


APK Lab VScode extension is used to reverse engineer. One of the best free tools for reverse engineering (decoding the APK)



Being defensive
1. Check for GPS mock locations
	```java
	/**
     * Returns true if this location is marked as a mock location. If this location comes from the
     * Android framework, this indicates that the location was provided by a test location provider,
     * and thus may not be related to the actual location of the device.
     *
     * @see LocationManager#addTestProvider
     */
    public boolean isMock() {
        return (mFieldsMask & HAS_MOCK_PROVIDER_MASK) != 0;
    }
```
2. Always act based on the error HTTP responses. 
	Log out if the API is unauthorised. 

3. Use local storage wisely

	a. **Shared Preferences and External storage** 
		- Do not store any credentials here
		- Do not store certificates (public or private)
		- Do not store encryption keys
		- Do not store device information (name, serial, etc)
	b. **Encrypted Shared preferences** 
		- Confidential data may be stored here
		- Segment distinct use cases into separate ESP files. 
		- ESP files with unique encryption keys should be stored in keystore. 
		- Long lived refresh token may be stored but must live in a dedicated ESP file
		- Each ESP file must have its own master key, specify a unique keyAlias for each file
		- All encryption key material must be stored in the KeyStore.
		- Remove all confidential data in log out or device de-registration.
	c. **Keystore**
		- All Encryption key material should be stored in keystore
		- Require biometric authentication (if available) for highly confidential data
		- Use the highest key security level supported by the OS version and device hardware
		- You should use the `setUnlockedDeviceRequired` for critical, highly confidential and restricted data
		- You should use `setUserAuthenticationRequired` for all other data classifications.

4. Use NDK
	- Native development kit (using c/c++ code to store keys)
	-  Machine code does not provide security as it can also be decompiled. It would add an extra step  and difficulty to retrieve desired information so it is a useful tip to use instead of hardcoding something into java/kotlin class

5. APK signature Check
	1. [Android/verified-installation/verified-installation-impl/src/main/java/com/duckduckgo/verifiedinstallation/certificate/SigningCertificateHashExtractor.kt at 93fe83393ab250e68290458efded42017bbf2fb5 · duckduckgo/Android · GitHub](https://github.com/duckduckgo/Android/blob/93fe83393ab250e68290458efded42017bbf2fb5/verified-installation/verified-installation-impl/src/main/java/com/duckduckgo/verifiedinstallation/certificate/SigningCertificateHashExtractor.kt)
6. Abstract important algorithms to backend
7. Everything relies on a secure OS 
	1. Root detection


All of the proposed ideas are adding more time and difficulty needed for an attacker to reverse engineer an application. 
Attackers with enough time, financial resources and determination still have high chances of accessing intended code/data

Have a threat model and develop your application with the remediations necessary to accomplish your goals. 
