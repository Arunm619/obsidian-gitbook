


``` Full ANR Stack Trace
0.110  E  ANR in com.franjam.anr.demo (com.franjam.anr.demo/com.franjam.anr.ui.ANRDemoActivity)
                 PID: 27596
                 Reason: Input dispatching timed out (3c2b837 com.franjam.anr.demo/com.franjam.anr.ui.ANRDemoActivity (server) is not responding. Waited 5003ms for FocusEvent(hasFocus=false))
                 Parent: com.franjam.anr.demo/com.franjam.anr.ui.ANRDemoActivity
                 ErrorId: 3881dc1a-1fd1-46b4-b9c3-da5ea219afcd
                 Frozen: false
                 Load: 3.72 / 4.2 / 4.81
                 ----- Output from /proc/pressure/memory -----
                 some avg10=0.00 avg60=0.03 avg300=0.04 total=8788014
                 full avg10=0.00 avg60=0.00 avg300=0.00 total=2245200
                 ----- End output from /proc/pressure/memory -----
                 
                 CPU usage from 1ms to 5200ms later (2024-03-05 17:22:34.849 to 2024-03-05 17:22:40.049) with 99% awake:
                   174% 2953/com.google.android.apps.nexuslauncher: 109% user + 65% kernel / faults: 192874 minor
                   122% 27596/com.franjam.anr.demo: 100% user + 21% kernel / faults: 694662 minor 41 major
                   14% 1757/system_server: 5.7% user + 8.2% kernel / faults: 3853 minor 35 major
                   0% 1337/media.codec: 0% user + 0% kernel / faults: 11038 minor 14 major
                   9.7% 3945/com.google.android.inputmethod.latin: 5.5% user + 4.2% kernel / faults: 1312 minor 14 major
                   6.3% 5088/com.android.bluetooth: 3.6% user + 2.6% kernel / faults: 2168 minor 29 major
                   5.5% 2375/com.android.systemui: 3.6% user + 1.9% kernel / faults: 1455 minor 6 major
                   3.6% 3063/com.google.android.gms.persistent: 2.3% user + 1.3% kernel / faults: 1311 minor 6 major
                   0% 1485/media.swcodec: 0% user + 0% kernel / faults: 3388 minor 13 major
                   2.6% 1117/surfaceflinger: 0.9% user + 1.7% kernel / faults: 609 minor 1 major
                   2.4% 1248/adbd: 0.9% user + 1.5% kernel / faults: 257 minor
                   2.1% 764/loop4: 0% user + 2.1% kernel
                   0% 148/kswapd0: 0% user + 0% kernel
                   1.7% 2681/com.android.phone: 0.7% user + 0.9% kernel / faults: 904 minor 18 major
                   0% 2555/.qtidataservices: 0% user + 0% kernel / faults: 1213 minor 16 major
                   1.3% 644/logd: 0.3% user + 0.9% kernel / faults: 81 minor
                   1.3% 1312/media.extractor: 0.5% user + 0.7% kernel / faults: 1644 minor 14 major
                   1.3% 25931/kworker/u16:7: 0% user + 1.3% kernel
                   1.1% 2499/com.android.networkstack.process: 1.1% user + 0% kernel / faults: 845 minor 2 major
                   1.1% 2644/org.codeaurora.ims: 0.7% user + 0.3% kernel / faults: 1181 minor 11 major
                   0% 2665/com.google.android.apps.cbrsnetworkmonitor: 0% user + 0% kernel / faults: 1077 minor 10 major
                   0% 2723/.dataservices: 0% user + 0% kernel / faults: 1156 minor 11 major
                   1.1% 3744/com.android.nfc: 0.5% user + 0.5% kernel / faults: 1006 minor 4 major
                   0% 3784/org.lineageos.settings.doze: 0% user + 0% kernel / faults: 1093 minor 10 major
                   1.1% 26920/kworker/u17:3: 0% user + 1.1% kernel
                   0% 2643/com.qti.phone: 0% user + 0% kernel / faults: 974 minor 3 major
                   0.9% 2647/com.android.se: 0.5% user + 0.3% kernel / faults: 1058 minor 7 major
                   0% 3736/com.android.bluetooth.bthelper: 0% user + 0% kernel / faults: 1108 minor 8 major
                   0% 3803/com.android.touch.gestures: 0% user + 0% kernel / faults: 1156 minor 9 major
                   0% 3820/org.pixelexperience.faceunlock: 0% user + 0% kernel / faults: 1037 minor 8 major
                   0.9% 22601/kworker/u16:3: 0% user + 0.9% kernel
                   0.9% 25933/kworker/u16:9: 0% user + 0.9% kernel
                   0.9% 27749/logcat: 0.3% user + 0.5% kernel
                   0% 623/loop0: 0% user + 0% kernel
                   0.7% 25930/kworker/u16:5: 0% user + 0.7% kernel
                   0.5% 465/usbtemp_kthread: 0% user + 0.5% kernel
                   0% 753/tombstoned: 0% user + 0% kernel / faults: 26 minor 44 major
                   0.5% 773/loop9: 0% user + 0.5% kernel
                   0% 777/loop11: 0% user + 0% kernel
                   0.5% 10453/kworker/u17:2: 0% user + 0.5% kernel
                   0.5% 27455/process-tracker: 0.1% user + 0.3% kernel
                   0.3% 1/init: 0% user + 0.3% kernel
                   0% 19/ksoftirqd/1: 0% user + 0% kernel
                   0% 775/loop10: 0% user + 0% kernel
                   0% 811/loop20: 0% user + 0% kernel
                   0.3% 1014/android.hardware.bluetooth@1.0-service-qti: 0.3% user + 0% kernel / faults: 2 minor
                   0.3% 1318/mediaserver: 0% user + 0.3% kernel / faults: 35 minor
                   0.3% 27453/process-tracker: 0% user + 0.3% kernel
17:22:40.110  E    0.3% 27520/com.android.vending: 0.3% user + 0% kernel / faults: 155 minor
                   0.3% 27797/com.Slack: 0.3% user + 0% kernel / faults: 105 minor
                   0.1% 9/rcu_preempt: 0% user + 0.1% kernel
                   0.1% 10/rcu_sched: 0% user + 0.1% kernel
                   0.1% 12/rcuop/0: 0% user + 0.1% kernel
                   0% 13/rcuos/0: 0% user + 0% kernel
                   0.1% 15/migration/0: 0% user + 0.1% kernel
                   0% 26/migration/2: 0% user + 0% kernel
                   0.1% 30/rcuop/2: 0% user + 0.1% kernel
                   0.1% 46/rcuop/4: 0% user + 0.1% kernel
                   0% 50/migration/5: 0% user + 0% kernel
                   0% 51/ksoftirqd/5: 0% user + 0% kernel
                   0% 63/rcuos/6: 0% user + 0% kernel
                   0.1% 274/kgsl_worker_thr: 0% user + 0.1% kernel
                   0% 388/irq/533-limits_: 0% user + 0% kernel
                   0% 574/kworker/3:1H: 0% user + 0% kernel
                   0.1% 657/vold: 0.1% user + 0% kernel / faults: 45 minor 6 major
                   0.1% 716/keystore2: 0% user + 0.1% kernel / faults: 35 minor 1 major
                   0.1% 903/statsd: 0.1% user + 0% kernel / faults: 90 minor 3 major
                   0.1% 904/netd: 0% user + 0.1% kernel / faults: 61 minor 3 major
                   0.1% 1012/als_correction_service: 0% user + 0.1% kernel
                   0.1% 1038/android.hardware.sensors@2.0-service.multihal: 0% user + 0.1% kernel
                   0.1% 1046/vendor.qti.hardware.display.allocator-service: 0% user + 0.1% kernel
                   0.1% 1104/audioserver: 0% user + 0.1% kernel / faults: 47 minor 1 major
                   0% 1251/drmserver: 0% user + 0% kernel / faults: 35 minor 8 major
                   0.1% 1304/cameraserver: 0% user + 0.1% kernel / faults: 82 minor 6 major
                   0.1% 1640/msm_irqbalance: 0% user + 0.1% kernel
                   0.1% 3411/cds_ol_rx_threa: 0% user + 0.1% kernel
                   0.1% 22605/kworker/u17:5: 0% user + 0.1% kernel
                   0.1% 24937/kworker/u17:6: 0% user + 0.1% kernel
                   0.1% 25870/kworker/0:1: 0% user + 0.1% kernel
                   0.1% 25951/kworker/2:3: 0% user + 0.1% kernel
                   0.1% 26013/kworker/1:3: 0% user + 0.1% kernel
                 52% TOTAL: 32% user + 18% kernel + 1.2% iowait + 0.4% irq + 0.4% softirq
                 CPU usage from 54ms to 380ms later (2024-03-05 17:22:34.903 to 2024-03-05 17:22:35.228):
                   189% 2953/com.google.android.apps.nexuslauncher: 126% user + 63% kernel / faults: 3061 minor
                     98% 2963/ReferenceQueueD: 51% user + 47% kernel
                     75% 2953/s.nexuslauncher: 67% user + 7.9% kernel
                     7.9% 2981/launcher-loader: 3.9% user + 3.9% kernel
                     7.9% 3909/RenderThread: 3.9% user + 3.9% kernel
                   152% 27596/com.franjam.anr.demo: 134% user + 18% kernel / faults: 30231 minor
                     97% 27596/ranjam.anr.demo: 87% user + 9.2% kernel
                     50% 27611/HeapTaskDaemon: 41% user + 9.2% kernel
                   22% 1757/system_server: 7.6% user + 15% kernel / faults: 611 minor
                     26% 27957/AnrConsumer: 11% user + 15% kernel
                   3% 15/migration/0: 0% user + 3% kernel
                   3.3% 465/usbtemp_kthread: 0% user + 3.3% kernel
                   3.6% 1117/surfaceflinger: 0% user + 3.6% kernel
                   3.9% 3063/com.google.android.gms.persistent: 3.9% user + 0% kernel / faults: 3 minor
                   4.1% 5088/com.android.bluetooth: 0% user + 4.1% kernel / faults: 3 minor
                   4.4% 24937/kworker/u17:6: 0% user + 4.4% kernel
                 46% TOTAL: 32% user + 14% kernel + 0.3% irq

```

---

The ANR (Application Not Responding) stacktrace you provided can be broken down into several sections. Here's a summary in table format:

| Section         | Description                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| General Info    | The ANR occurred in `com.franjam.anr.demo` during `com.franjam.anr.ui.ANRDemoActivity`. The PID (Process ID) is `27596`. The reason is that input dispatching timed out because the server is not responding. The error ID is `3881dc1a-1fd1-46b4-b9c3-da5ea219afcd`. The system load at the time was `3.72 / 4.2 / 4.81`. |
| Memory Pressure | The output from `/proc/pressure/memory` shows some memory pressure, but it's not severe.                                                                                                                                                                                                                                   |
| CPU Usage       | The CPU usage from `1ms` to `5200ms` later shows that the app `com.franjam.anr.demo` was using `122%` of the CPU, which is quite high. This could be the cause of the ANR.                                                                                                                                                 |

To resolve this issue, you should investigate why `com.franjam.anr.demo` is using so much CPU. The code you provided shows a long-running method that sorts a large array. This operation could be causing the high CPU usage. Consider optimizing this method or running it in a background thread to prevent blocking the UI thread and causing an ANR.