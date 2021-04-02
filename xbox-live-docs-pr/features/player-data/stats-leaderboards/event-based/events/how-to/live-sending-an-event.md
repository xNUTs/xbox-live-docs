---
title: Sending an event
description: Example code for sending an event, for event-based Stats & Leaderboards.
kindex: Sending an event
author: v-mihof
ms.author: v-mihof
ms.topic: conceptual
ms.prod: gaming
ms.technology: xboxlive
ms.localizationpriority: medium
ms.date: 09/14/2017
edited: 00/00/0000
---

# Sending an event

This example code shows how to write an event.
On the service, this will update event-based stats based on the stat rules you've defined in Partner Center.


**C API**
<!-- XblEventsWriteInGameEvent.md -->
```cpp
HRESULT hr = XblEventsWriteInGameEvent(
    xboxLiveContext,
    "PuzzleSolved",
    R"({"DifficultyLevelId":100, "GameplayModeId":"Adventure"})",
    R"({"LocationX":1,"LocationY":1})"
);
```

<!-- **Reference**
* [XblEventsWriteInGameEvent](xbleventswriteingameevent.md) -->
