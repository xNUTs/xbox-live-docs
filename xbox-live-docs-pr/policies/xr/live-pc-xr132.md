---
title: "XR-132: Service Access Limitations"
description: Titles which exceed limits when calling Xbox Live services, or do not adhere to retry policies, may be subjected to rate limiting.
ms.topic: article
keywords: windows 10, uwp, games, xbox, xbox live, policies
ms.localizationpriority: medium
ms.date: 03/18/2019
---

# XR-132: Service Access Limitations

Titles which exceed [title and user based limits](https://docs.microsoft.com/windows/uwp/xbox-live/using-xbox-live/best-practices/fine-grained-rate-limiting) when calling Xbox Live services or do not adhere to Xbox Live service retry policies may be subjected to rate limiting, which may result in service interruption or deprecation.
Failure to adhere to the specified limits may block a title from release, and in-production issues with released titles may result in Xbox Live services suspension up to and including title removal.


## Recommended Test Cases


### 132-01 Service Access Limitations


#### Tools Needed

1. Fiddler
2. [Xbox Live Trace Analyzer](https://aka.ms/xboxlivetoolspackage) to parse the output files from Fiddler


#### Test Steps

1. With the title running, start a fiddler trace and proceed to move through all areas of the title, including (if supported), but not limited to, the following:
    * Create a game save, reboot the device and load the game save.
    * Change rich presence states in quick succession (if possible).
    * Unlock and view achievements.
    * Post to all leaderboards and view all leaderboards using all filters.
    * View in-game Friends List (including a friend with presence blocked) and move between pages rapidly.
    * Earn and view a Hero Stat.
    * Match-make into all online modes, including being unable to find an available session (if possible) and generate voice traffic.
    * Create, save and share a game clip.
    * Access the in-game store (if applicable).

2. Once test has concluded, stop the fiddler trace.

3. In the XDK command prompt, run the following:

   `xboxlivetraceanalyzer -data filepath -outputdir filepath`

4. Open the output directory from the above step and open the ‘index’ file. If prompted, select **Allow blocked content**.


#### Expected Result

Games must not display any serious warnings in their Live Trace Analyzer output results. Titles must ensure they keep their service calls to Xbox Live endpoints below the specified burst and sustain limits.


#### Pass Examples

* The title does not exceed the sustain limit when calling Xbox Live services.  


#### Fail Examples

* The title exceeds the sustain limit (limit at which rate limiting takes effect) by 10x. For example, if the sustained limit at which Fine Grain Rate Limiting takes effect is set to 300 calls in 300 seconds, titles at or above 3000 calls in 300 seconds will fail.
