---
title: Handling a title Presence change
description: Example code for handling a title Presence change.
kindex: Handling a title Presence change
kindex: Presence
ms.topic: conceptual
ms.localizationpriority: high
author: mikehoffms
ms.author: v-mihof
ms.date: 01/09/2020
---


# Handling a title Presence change


## Subscribing to a title presence change


**C API**
<!--  XblPresenceSubscribeToTitlePresenceChange_C.md -->
<!-- note guid "123" -->
```cpp
uint64_t xuid{ 123 };

HRESULT hr = XblPresenceSubscribeToTitlePresenceChange(
    xboxLiveContext,
    xuid,
    titleId,
    &state.titlePresenceChangeSubscription
);
```

<!--**Reference**
* [XblPresenceSubscribeToTitlePresenceChange](xblpresencesubscribetotitlepresencechange.md)-->


## Unsubscribing from a title presence change


**C API**
<!--  XblPresenceUnsubscribeFromTitlePresenceChange_C.md -->
```cpp
HRESULT hr = XblPresenceUnsubscribeFromTitlePresenceChange(
    xboxLiveContext,
    state.titlePresenceChangeSubscription
);

state.titlePresenceChangeSubscription = nullptr;
```

<!--**Reference**
* [XblPresenceUnsubscribeFromTitlePresenceChange](xblpresenceunsubscribefromtitlepresencechange.md)-->


## Adding a title presence change handler


**C API**
<!--  XblPresenceAddTitlePresenceChangedHandler_C.md -->
```cpp
state.titlePresenceChangedHandlerToken =  XblPresenceAddTitlePresenceChangedHandler(
    xboxLiveContext,
    [](void* context, uint64_t xuid, uint32_t titleId, XblPresenceTitleState titleState)
    {
        UNREFERENCED_PARAMETER(context);
        LogToFile("Title presence change notification received:");
        LogToFile("Xuid = %u, titleId = %u, titleState = %u", xuid, titleId, titleState);
    },
    nullptr
);
```

<!--**Reference**
* [XblPresenceAddTitlePresenceChangedHandler](xblpresenceaddtitlepresencechangedhandler.md)
* [XblPresenceTitleState](xblpresencetitlestate.md)-->


## Removing a title presence change handler

**C API**
<!--  XblPresenceRemoveTitlePresenceChangedHandler_C.md -->
```cpp
HRESULT hr = XblPresenceRemoveTitlePresenceChangedHandler(
    xboxLiveContext,
    state.titlePresenceChangedHandlerToken
);

state.titlePresenceChangedHandlerToken = 0;
```

<!--**Reference**
* [XblPresenceRemoveTitlePresenceChangedHandler](xblpresenceremovetitlepresencechangedhandler.md)-->
