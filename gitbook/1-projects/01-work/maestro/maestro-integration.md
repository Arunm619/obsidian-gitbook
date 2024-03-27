
Commands:

 `maestro studio` - this is used for creating flows. Studio is a webapp that opens up with emulator that helps us with flow creation with show and create model.


`maestro test buynow.yaml` - Executes the flow written in yaml file


```terminal
flashlight test --bundleId com.meesho.supply.debug \
  --testCommand " maestro test homepagescrolldemo.yaml" \
  --iterationCount 3 \
  --resultsFilePath results.json
```

[22:13:18] ℹ️  Installing C++ profiler for arm64-v8a architecture
[22:13:18] ✅  C++ Profiler installed in /data/local/tmp/BAMPerfProfiler
[22:13:19] ℹ️  Running iteration 1/3
Running on 192.168.1.6:39405

Running on 192.168.1.6:39405
 > Flow

Launch app "com.meesho.supply.debug"...
 COMPLETED

Scroll vertically...
 COMPLETED

Scroll vertically...
 COMPLETED

[22:14:07] ✅  Finished iteration 1/3 in 7960.464040994644ms (0 retry so far)
[22:14:07] ℹ️  Running iteration 2/3
Running on 192.168.1.6:39405

Running on 192.168.1.6:39405
 > Flow

Launch app "com.meesho.supply.debug"...
 COMPLETED

Scroll vertically...
 COMPLETED
Scroll vertically...
 COMPLETED

[22:15:06] ✅  Finished iteration 2/3 in 20242.730541944504ms (0 retry so far)
[22:15:06] ℹ️  Running iteration 3/3
Running on 192.168.1.6:39405

Running on 192.168.1.6:39405
 > Flow

Launch app "com.meesho.supply.debug"...
 COMPLETED

Scroll vertically...
 COMPLETED

Scroll vertically...
 COMPLETED

[22:15:51] ✅  Finished iteration 3/3 in 8428.877499818802ms (0 retry so far)
[22:15:51] ✅  Results written to results.json.
To open the web report, run:

flashlight report results.json
~/Work/maestro_ui_suit/flows/regression_suit/homepage main !2 ?2 ─────────────────────── 2m 35s 10:15:52 PM
❯ flashlight report results.json

[22:15:59] ✅  Opening report: /var/folders/ng/0gkd8zf17ss78t782gtp7vsr0000gp/T/report.html
~/Work/maestro_ui_suit/flows/regression_suit/homepage main !2 ?2 ────────────────────────────── 10:15:59 PM


