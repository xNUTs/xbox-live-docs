---
title: "XR-074: Loss of Connectivity to Xbox and Partner Services"
description: Titles must resolve errors with Xbox Live and partner services connectivity.
kindex: "XR-074: Loss of Connectivity to Xbox and Partner Services &diams;"
kindex: policies
ms.topic: article
ms.localizationpriority: medium
ms.date: 03/18/2019
---

# XR-074: Loss of Connectivity to Xbox and Partner Services

Titles must resolve errors with Xbox Live and partner services connectivity. Titles must honor the retry policies set by Xbox Live when attempting to retry a request to the Xbox service after a failure has occurred.  Titles must appropriately manage messaging the user when services are unavailable. For example, if a partner service other than Xbox Live is not available, the game should not indicate that there is an issue with Xbox Live.


## More Information


### Handling Issues With Non Xbox Live Services

Titles encountering issues with partner services such as non-transient timeouts, network API errors, or missing service configuration that impacts the user experience should alert the user to the specific feature or service that is unavailable. Titles should fail gracefully to a safe state while the user troubleshoots, or to a state in which the user can manually retry.

An example of a user-friendly message is:

>"Sorry, _non-Microsoft service_ is not currently available. Please try again later. For more information, contact _non-Microsoft support contact information_."


### Handling Issues With Xbox Live Services

Some functionality might become unavailable if connectivity to an Xbox service is lost. In such instances, titles should use clear, user-friendly messaging to communicate this to users.

If a service is unavailable, titles are permitted to retry their request, but they can do so only within the parameters allowed by Xbox Live. For more information about service resiliency for Xbox One titles, including required HTTP retry and back-off logic, as well as user-interaction guidance for individual services, see Service Interruption Resiliency for Titles.


## Recommended Test Cases


### 074-01 WAN Disconnection to Xbox Services

#### Test Steps

1. Sign into an Xbox profile.

2. While performing the following actions, disconnect the WAN network (if using an Ethernet switch/hub disconnect the uplink cable from the network device. If the device is connected via Wifi, disconnect the uplink cable from the wireless access point) connection:
    * Creating a new save point.
    * Loading a save point.
    * Reaching an auto-save point.
    * Enumerating a list of saved games.
    * Searching for and joining an online session.
    * Attempting to create an online session.
    * Viewing a leaderboard (if applicable).
    * Playing offline.


#### Expected Result

In the event that the device is unable to reach Xbox services, the title should respond with a user-friendly error message.


#### Pass Examples

1. Title displays error message indicating loss of network connection to Xbox services.

2. Title does not display an error message while playing a local game mode that does not require Xbox.


#### Fail Examples

1. User is unable to complete a non-online Xbox game session.

2. Title goes into an unresponsive or unstable state.


### 074-02 Direct Disconnection


#### Test Steps

1. Sign into an Xbox profile.

2. While performing the following actions in the title, pull the network cable from the device or power off the WAP or wireless router:
    * Creating a new save point.
    * Loading a save point.
    * Reaching an auto-save point.
    * Enumerating a list of saved games.
    * Searching for and joining an online session.
    * Attempting to create an online session.
    * Viewing a leaderboard (if applicable).
    * Playing offline.


#### Expected Result

In the event the device loses connection to Xbox services, the title should respond with a user-friendly error message.


#### Pass Examples

1. The title displays a user-friendly message while in online game mode.

2. The title does not interrupt game-play during offline game mode.


#### Fail Examples

1. An error message is displayed during offline game mode.

2. The user is able to view online menus or view buffered media after the network goes offline.


### 074-07 Dynamic Connectivity Loss


#### Tools Needed

* Fiddler


#### Test Steps

1. Sign into an Xbox profile and launch the title.
2. Access non-Microsoft online feature.
3. Use Fiddler to emulate downtime.


#### Expected Results

Title should gracefully handle disconnections to non-Microsoft service.


#### Pass Examples

1. Title does not hang or crash upon loss of connectivity to the partner-hosted service.


#### Fail Examples

1. Error displayed implies issues with Microsoft service.
2. Non-descriptive error message is displayed.
3. Title crashes or becomes unstable.


### 074-08 Pre-launch Downtime


#### Tools Needed

* Fiddler


#### Test Steps

1. Use Fiddler to emulate downtime. 

2. Sign into an Xbox profile and launch the title.

3. Access non-Microsoft online feature.


#### Expected Results

Titles should provide a user-friendly error message indicating that there is a problem reaching the non-Microsoft service and should allow an opportunity to retry connection.


#### Pass Examples

1. Title does not hang or crash upon loss of connectivity to the partner-hosted service.


#### Fail Examples

1. Error displayed implies issues with Microsoft service.
2. Non-descriptive error message is displayed.
3. Title crashes or becomes unstable.
