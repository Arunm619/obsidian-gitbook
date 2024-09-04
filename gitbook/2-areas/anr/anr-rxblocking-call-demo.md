

```
ANR in com.franjam.anr.demo (com.franjam.anr.demo/com.franjam.anr.ui.ANRDemoActivity)
                 PID: 28565
                 Reason: Input dispatching timed out (b92464f com.franjam.anr.demo/com.franjam.anr.ui.ANRDemoActivity (server) is not responding. Waited 5005ms for MotionEvent)
                 Parent: com.franjam.anr.demo/com.franjam.anr.ui.ANRDemoActivity
                 ErrorId: bb732620-9b4f-40ee-a39b-0224b1ee7272
                 Frozen: false
                 Load: 3.32 / 3.44 / 4.29
                 ----- Output from /proc/pressure/memory -----
                 some avg10=0.00 avg60=0.00 avg300=0.00 total=8880064
                 full avg10=0.00 avg60=0.00 avg300=0.00 total=2272668
                 ----- End output from /proc/pressure/memory -----
                 
                 CPU usage from 50650ms to 0ms ago (2024-03-05 17:27:07.192 to 2024-03-05 17:27:57.843):
                   199% 2953/com.google.android.apps.nexuslauncher: 128% user + 70% kernel / faults: 1289215 minor
                   8% 1117/surfaceflinger: 5.1% user + 2.9% kernel / faults: 419 minor
                   5.4% 1757/system_server: 3.6% user + 1.7% kernel / faults: 22002 minor
                   1.7% 1030/android.hardware.graphics.composer@2.4-service: 1.1% user + 0.6% kernel / faults: 40 minor
                   1.4% 2375/com.android.systemui: 0.8% user + 0.5% kernel / faults: 1827 minor
                   1.2% 1248/adbd: 0.3% user + 0.8% kernel / faults: 1051 minor
                   0.8% 525/crtc_commit:139: 0% user + 0.8% kernel
                   0.8% 25933/kworker/u16:9: 0% user + 0.8% kernel
                   0.7% 274/kgsl_worker_thr: 0% user + 0.7% kernel
                   0.6% 25927/kworker/u16:1: 0% user + 0.6% kernel
                   0.5% 3063/com.google.android.gms.persistent: 0.4% user + 0.1% kernel / faults: 731 minor
                   0.5% 27453/process-tracker: 0.1% user + 0.4% kernel
                   0.5% 27455/process-tracker: 0.1% user + 0.4% kernel
                   0.5% 5088/com.android.bluetooth: 0.4% user + 0% kernel / faults: 1229 minor
                   0.5% 25930/kworker/u16:5: 0% user + 0.5% kernel
                   0.4% 3380/com.google.android.gms: 0.3% user + 0.1% kernel / faults: 2761 minor 3 major
                   0.4% 148/kswapd0: 0% user + 0.4% kernel
                   0.4% 465/usbtemp_kthread: 0% user + 0.4% kernel
                   0.4% 644/logd: 0.2% user + 0.2% kernel / faults: 208 minor
                   0.3% 3166/irq/33-90cd000.: 0% user + 0.3% kernel
                   0.3% 28074/com.google.android.googlequicksearchbox:search: 0.2% user + 0% kernel / faults: 567 minor
                   0.3% 1014/android.hardware.bluetooth@1.0-service-qti: 0.1% user + 0.1% kernel
                   0.3% 3685/com.google.android.as: 0.2% user + 0% kernel / faults: 3872 minor
                   0.3% 25979/kworker/u17:0: 0% user + 0.3% kernel
                   0.3% 1038/android.hardware.sensors@2.0-service.multihal: 0.1% user + 0.1% kernel
                   0.2% 903/statsd: 0.2% user + 0% kernel / faults: 160 minor
                   0.2% 27749/logcat: 0.1% user + 0.1% kernel
                   0.2% 98/system: 0% user + 0.2% kernel
                   0.2% 22605/kworker/u17:5: 0% user + 0.2% kernel
                   0.2% 3164/irq/32-90b6400.: 0% user + 0.2% kernel
                   0.1% 645/lmkd: 0% user + 0.1% kernel
                   0.1% 1012/als_correction_service: 0% user + 0.1% kernel
                   0.1% 1/init: 0.1% user + 0% kernel
                   0.1% 9/rcu_preempt: 0% user + 0.1% kernel
                   0.1% 526/crtc_event:139: 0% user + 0.1% kernel
                   0.1% 1046/vendor.qti.hardware.display.allocator-service: 0% user + 0.1% kernel
                   0.1% 1640/msm_irqbalance: 0% user + 0.1% kernel
                   0.1% 24937/kworker/u17:6: 0% user + 0.1% kernel
                   0.1% 28314/irq/308-touchpa: 0% user + 0.1% kernel
                   0.1% 27797/com.Slack: 0.1% user + 0% kernel / faults: 304 minor
                   0.1% 739/f2fs_ckpt-252:2: 0% user + 0.1% kernel
                   0% 12/rcuop/0: 0% user + 0% kernel
                   0% 30/rcuop/2: 0% user + 0% kernel
                   0% 1304/cameraserver: 0% user + 0% kernel
                   0% 25870/kworker/0:1: 0% user + 0% kernel
                   0% 905/zygote64: 0% user + 0% kernel / faults: 135 minor
                   0% 26349/kworker/3:6: 0% user + 0% kernel
                   0% 26920/kworker/u17:3: 0% user + 0% kernel
                   0% 28342/com.google.android.webview:sandboxed_process0:org.chromium.content.app.SandboxedProcessService0:0: 0% user + 0% kernel / faults: 412 minor 1 major
                   0% 1031/android.hardware.health@2.1-service: 0% user + 0% kernel
                   0% 25931/kworker/u16:7: 0% user + 0% kernel
                   0% 26013/kworker/1:3: 0% user + 0% kernel
                   0% 19/ksoftirqd/1: 0% user + 0% kernel
                   0% 38/rcuop/3: 0% user + 0% kernel
                   0% 582/ueventd: 0% user + 0% kernel
                   0% 646/servicemanager: 0% user + 0% kernel
17:28:01.640  E    0% 904/netd: 0% user + 0% kernel / faults: 123 minor
                   0% 1040/android.hardware.wifi@1.0-service: 0% user + 0% kernel / faults: 4 minor
                   0% 1104/audioserver: 0% user + 0% kernel / faults: 4 minor
                   0% 2499/com.android.networkstack.process: 0% user + 0% kernel / faults: 20 minor
                   0% 2764/webview_zygote: 0% user + 0% kernel / faults: 48 minor
                   0% 3411/cds_ol_rx_threa: 0% user + 0% kernel
                   0% 3945/com.google.android.inputmethod.latin: 0% user + 0% kernel / faults: 42 minor
                   0% 25951/kworker/2:3: 0% user + 0% kernel
                   0% 28257/kworker/0:2: 0% user + 0% kernel
                   0% 28341/com.google.android.webview:webview_service: 0% user + 0% kernel / faults: 605 minor
                   0% 8/ksoftirqd/0: 0% user + 0% kernel
                   0% 10/rcu_sched: 0% user + 0% kernel
                   0% 22/rcuop/1: 0% user + 0% kernel
                   0% 46/rcuop/4: 0% user + 0% kernel
                   0% 54/rcuop/5: 0% user + 0% kernel
                   0% 62/rcuop/6: 0% user + 0% kernel
                   0% 497/core_ctl/7: 0% user + 0% kernel
                   0% 647/hwservicemanager: 0% user + 0% kernel
                   0% 715/android.system.suspend@1.0-service: 0% user + 0% kernel
                   0% 741/f2fs_discard-25: 0% user + 0% kernel
                   0% 811/loop20: 0% user + 0% kernel
                   0% 837/loop26: 0% user + 0% kernel
                   0% 895/ipacm: 0% user + 0% kernel
                   0% 1064/vendor.qti.hardware.vibrator.service.oplus: 0% user + 0% kernel / faults: 44 minor
                   0% 1066/qrtr_rx: 0% user + 0% kernel
                   0% 1325/wificond: 0% user + 0% kernel
                   0% 1619/qcrild: 0% user + 0% kernel
                   0% 1635/qcrild: 0% user + 0% kernel
                   0% 2681/com.android.phone: 0% user + 0% kernel / faults: 10 minor
                   0% 3409/scheduler_threa: 0% user + 0% kernel
                   0% 3670/com.android.providers.media.module: 0% user + 0% kernel / faults: 2 major
                   0% 3744/com.android.nfc: 0% user + 0% kernel / faults: 2 minor
                   0% 22057/kworker/0:3: 0% user + 0% kernel
                   0% 25205/com.what3words.android: 0% user + 0% kernel / faults: 2 minor
                   0% 25950/kworker/2:0: 0% user + 0% kernel
                   0% 26018/kworker/5:4: 0% user + 0% kernel
                   0% 26022/kworker/6:6: 0% user + 0% kernel
                   0% 26545/kworker/7:0: 0% user + 0% kernel
                  +0% 28565/com.franjam.anr.demo: 0% user + 0% kernel
                  +0% 28623/com.google.android.apps.photos: 0% user + 0% kernel
                  +0% 28624/com.meesho.supply.debug: 0% user + 0% kernel
                  +0% 28779/com.google.android.webview:sandboxed_process0:org.chromium.content.app.SandboxedProcessService0:0: 0% user + 0% kernel
                  +0% 28864/kworker/3:0: 0% user + 0% kernel
                 30% TOTAL: 19% user + 10% kernel + 0% iowait + 0.3% irq + 0.1% softirq
                 CPU usage from 42ms to 371ms later (2024-03-05 17:27:57.884 to 2024-03-05 17:27:58.213):
                   194% 2953/com.google.android.apps.nexuslauncher: 142% user + 51% kernel / faults: 2721 minor
                     99% 2963/ReferenceQueueD: 55% user + 43% kernel
                     79% 2953/s.nexuslauncher: 79% user + 0% kernel
                     7.9% 2981/launcher-loader: 3.9% user + 3.9% kernel
                     7.9% 3909/RenderThread: 3.9% user + 3.9% kernel
                   26% 1757/system_server: 3.8% user + 23% kernel / faults: 587 minor
                     23% 28878/AnrConsumer: 3.8% user + 19% kernel
                   3.5% 1038/android.hardware.sensors@2.0-service.multihal: 0% user + 3.5% kernel
                   3.6% 1117/surfaceflinger: 3.6% user + 0% kernel
                   4.5% 27749/logcat: 4.5% user + 0% kernel
                 28% TOTAL: 19% user + 9.3% kernel + 0.3% irq
```

