
Android is an open-source operating system based on the Linux kernel, primarily used in mobile devices like smartphones and tablets. It is developed by Google and the Open Handset Alliance. Here are some key components of Android's internals:

1. **Linux Kernel**: At the base of the Android software stack, the Linux Kernel provides a level of abstraction between the device hardware and the upper layers of the Android software stack. It handles core system services such as security, memory management, process management, network stack, and driver model.

2. **Android Runtime**: This includes the Dalvik Virtual Machine and Core Libraries which provide most of the functionality available in the core libraries of the Java programming language.

3. **Libraries**: These are a set of C/C++ libraries used by various components of the Android system. These libraries tell the device how to handle different kinds of data and are compiled to native code for better performance.

4. **Application Framework**: The Application Framework provides higher-level services to applications in the form of Java classes. It provides an abstraction layer for hardware access and manages the user interface and application resources.

5. **Applications**: All applications, both native and third-party, are built on the application layer using the same application framework. The applications include home, contact, settings, games, browsers etc.

6. **HAL (Hardware Abstraction Layer)**: HAL provides standard interfaces that expose device hardware capabilities to the higher-level Java API framework. HAL consists of multiple library modules, each of which implements an interface for a specific type of hardware component, such as the camera or bluetooth module.

7. **ART (Android Runtime)**: ART is the managed runtime used by applications and some system services on Android. ART and its predecessor Dalvik were originally created specifically for the Android project.

8. **System Server**: This runs core system services, such as WindowManager and PackageManager, that are used across multiple applications.

 Android's architecture is designed to be adaptable to a wide range of hardware and has a large community of developers creating applications to extend functionality.

----

Native applications in Android are those that are written using the Android Software Development Kit (SDK) and are typically written in Java or Kotlin. These applications are designed to run on the Android platform and can take full advantage of all the device features that the platform offers. Here are some examples:

1. **Google Maps**: This is a web mapping service developed by Google. It offers satellite imagery, aerial photography, street maps, 360° interactive panoramic views of streets, real-time traffic conditions, and route planning.

2. **Gmail**: This is a free email service developed by Google. Users can access Gmail on the web and using third-party programs that synchronize email content through POP or IMAP protocols.

3. **YouTube**: This is a video sharing service where users can watch, like, share, comment and upload their own videos. The video service can be accessed on PCs, laptops, tablets and via mobile phones.

4. **Google Drive**: This is a file storage and synchronization service developed by Google. It allows users to store files on their servers, synchronize files across devices, and share files.

5. **WhatsApp**: This is a free, multiplatform messaging app that lets you make video and voice calls, send text messages, and more — all with just a Wi-Fi connection.

6. **Instagram**: This is a photo and video sharing app that allows users to take pictures and videos, apply digital filters to them and share them on various social networking services.

7. **Facebook**: This is a popular free social networking website that allows registered users to create profiles, upload photos and video, send messages and keep in touch with friends, family and colleagues.

8. **Twitter**: This is an online news and social networking site where people communicate in short messages called tweets.

These are all examples of native Android applications. They are designed to work optimally on the Android platform, and they use Android's software stack to interact with the user and the device.

----

Third-party applications are those that are developed by developers other than the device's manufacturer. They are usually available for download from the Google Play Store or other Android app marketplaces. Here are some popular third-party applications for Android:

1. **Spotify**: A digital music, podcast, and video streaming service that gives you access to millions of songs and other content from artists all over the world.

2. **Netflix**: A streaming service that offers a wide variety of award-winning TV shows, movies, anime, documentaries, and more on thousands of internet-connected devices.

3. **Snapchat**: A multimedia messaging app used globally, created by Evan Spiegel, Bobby Murphy, and Reggie Brown, former students at Stanford University.

4. **Uber**: A ride-hailing app, offering services that include peer-to-peer ridesharing, ride service hailing, food delivery, and a micromobility system with electric bikes and scooters.

5. **Slack**: A cloud-based set of proprietary team collaboration tools and services.

6. **Zoom**: A videotelephony and online chat services through a cloud-based peer-to-peer software platform and is used for teleconferencing, telecommuting, distance education, and social relations.

7. **TikTok**: A social media app for creating and sharing videos as well as live broadcasting.

8. **Amazon Shopping**: The mobile application for the popular e-commerce website, Amazon.

9. **Evernote**: An app designed for note taking, organizing, task management, and archiving.

10. **WhatsApp**: A free, multiplatform messaging app that lets you make video and voice calls, send text messages, and more — all with just a Wi-Fi connection.

These applications are not pre-installed on the device and need to be downloaded by the user. They provide additional functionality that may not be available in the native applications.