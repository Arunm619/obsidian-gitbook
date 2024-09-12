
# Summary 

Calculate ANR (App Not Responding) rates with session backed data to match Google Play Console's Android vitals as closely as possible. The accepted solution is introducing a new, optional tag called `abnormal_mechanism` in the release health metrics dataset to track the type of ANR which will allow us to calculate the ANR rate without discrepancies introduced by client-side sampling. This tag will only be set by the Android SDK for sessions that experience an ANR event. We will be limiting the cardinality of the tag values; currently expecting to distinguish between background and foreground (user-perceived) ANRs, with a potential to extend to a third value to track AppHangs from iOS in the future.

# Motivation

ANR rate is an app health diagnostic (much like crash rate) that Google Play Console provides to allow developers to compare stability of releases. Google Play Console (platform that Google provides for developers to monitor the performance of their app, where they would find ANR rate) is not accessible to all developers on a project/team. We want to surface ANR rates and user-perceived ANR rates in Sentry to consolidate these app health diagnostics in one place.

# Background

ANRs are triggered if the UI thread on an Android app is blocked for too long. Android vitals provides the following [definition](https://developer.android.com/topic/performance/vitals/anr#android-vitals) for ANRs:

**ANR rate:** The percentage of your daily active users who experienced any type of ANR.

**User-perceived ANR rate:** The percentage of your daily active users who experienced at least one *user-perceived ANR*. Currently only ANRs of type `Input dispatching timed out` are considered user-perceived.

**Daily active user**: Unique user who uses your app on a single day on a single device, potentially over multiple sessions. If a user uses your app on more than one device in a single day, each device will contribute to the number of active users for that day. If multiple users use the same device in a single day, this is counted as one active user.

<aside>
💡 User-perceived ANR rate is a *core vital* meaning that it affects the discoverability of your app on Google Play.
</aside>
  

ANRs are currently surfaced as error events with tag `mechanism:ANR`. With the data we already have on hand, we can calculate ANR rate as follows:

```bash
(unique users who experienced error events with tag mechanism: ANR)
___________________________________________________________________
                    (total unique users)
```

There are a couple problems with this:

1. Total ANRs is affected by client side sampling and dropped events if org/project is close to error quota
2. The most accurate count of total unique users will probably come from the release health metrics dataset
3. Getting this information will require clickhouse queries to two different datasets and post-processing to calculate the ANR rate

Issues outlined in 1 & 2 will result in us showing *wrong* ANR rates and 3 will limit the capabilities of ANR rate - can’t allow sort and search, can’t add it to dashboards or alerts and is not future-proof in case we want to use ANR rates in issue detection.

