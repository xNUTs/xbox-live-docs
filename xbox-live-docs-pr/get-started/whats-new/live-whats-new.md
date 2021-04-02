---
title: What's new for Xbox Live
description: New features and functionality in each release of Xbox Live.
ms.topic: article
ms.localizationpriority: medium
ms.date: 10/23/2018
---

# What's new for Xbox Live

To see all of the recent code changes to the Xbox Live APIs, you can also check the <a href="https://github.com/Microsoft/xbox-live-api/commits/master" target="_blank">GitHub commit history for the "xbox-live-api" repo &#11008;</a>.

This article covers selected features and releases from 2017 through 2020.
For 2015 and 2016 releases, see the What's New article for that month, such as [What's new for the Xbox Live SDK - December 2016](archived/live-whats-new-1612.md).


<!-- ********************************************************************** -->
___
## June 2020


### Xbox Live Features


#### Multiplayer Activity (MPA)

The Multiplayer Activity (MPA) feature simplifies platform integration for player activities (joins), invites, and recent players.
The feature space will also allow players to launch into your game from their social graph, even if the title itself is not running.
Using MPA provides developers with increased opportunities for their user base to engage in social play and joinable multiplayer scenarios.

Important to note however, is that titles that wish to make use of MPA at this time must have their own session management systems, and not be dependent on use of MPSD.

See [Multiplayer Activity (MPA)](../../features/multiplayer/mpa/live-mpa-nav.md).


<!-- ********************************************************************** -->
___
## May 2020


### Xbox Live Features


#### Updating only the specified title-managed Stats

Previously, you had specify all of the stats in a single API call `XblTitleManagedStatsWriteAsync`.
Now, you can send specified stats that you want to update, by calling `XblTitleManagedStatsUpdateStatsAsync`, which selectively updates the calling user’s stats.
A specified stat will only be overwritten if it already exists; any stats that are not specified in the call to `XblTitleManagedStatsUpdateStatsAsync` will remain unchanged.

See [Writing title-managed stats](../../features/player-data/stats-leaderboards/title-managed/how-to/live-writing-tm-stats.md).


<!-- ********************************************************************** -->
___
## April 2020


### Xbox Live Features


#### Xbox Live PC Sandbox Switcher (XBLPCSandbox.exe)

[Xbox Live PC Sandbox Switcher (XBLPCSandbox.exe)](../../test-release/tools/live-pc-sandbox-switcher.md) is a command-line tool that helps manage the Xbox Live sandbox on PC.
This PC Sandbox Switcher can do the following:
* Show the name of the current sandbox.
* Set a sandbox to use.
* Re-launch the Microsoft Store app, the Xbox app, and the Xbox Companion app in sandbox mode.


#### New Multiplayer API: XblFormatSecureDeviceAddress

On platforms that don't have a secure device address, you can call the `XblFormatSecureDeviceAddress` function to generate a value that can be used by the `XblMultiplayerSessionCurrentUserSetSecureDeviceAddressBase64`
function.


#### Bug fixes

- Fixed an issue where the `XblTitleManagedStatsWriteAsync` function was not uploading stat values correctly.


<!-- ********************************************************************** -->
___
## November 2019


### Xbox Live Features


#### Xbox Live In-Game Event Writer for XSAPI C API

The Xbox Live In-Game Event Writer API is now available for XSAPI C API.
Developers can use the `XblEventsWriteInGameEvent` API to submit in-game events.  
<!-- Developers can use the [XblEventsWriteInGameEvent](xbleventswriteingameevent.md) API to submit in-game events.   -->


#### String Verify API is available now for XSAPI C API

When exposing a string to other players, it should be validated to ensure it doesn't violate the Code of Conduct or Terms of Use.
The String Verify API takes an array of strings and returns a result code for each one, indicating whether it is acceptable on, and a string containing the offending term.


<!-- #### Modern Gamertag related API updates

The Profile API, Leaderboards API, and Social Manager API have been updated to support modern gamertags.
For more information about modern gamertag, see the [modern gamertag](live-modern-gamertags-toc.md) section of the documentation. -->


<!-- ********************************************************************** -->
___
## September 2019


### Xbox Live Features


#### Xbox Live Title Storage feature is available now for XSAPI C API

Games can now use the Xbox Live Title Storage API.
Title Storage is cloud storage service for per-user or per-title data, such as player configurations or title assets.  


#### Xbox Live Title-managed Stats feature is available now for XSAPI C API

With title-managed Stats, the title keeps track of the stat values, and sends the values to the service to power out-of-game experiences such as Featured Stats.
Title-managed Stats was formerly known as Stats 2017.


<!-- ********************************************************************** -->
___
## October 2018


### Xbox Live Features

SDK is now available as precompiled binaries (libs), and integrated with a package manager for Android.
See [Getting started with the Xbox Live APIs on Android](../../get-started/setup-ide/managed-partners/astudio-android/other/live-android-get-started-xsapi.md).


### Fixes


#### XAL Fixes

- Xal's numerical parsing code has a chance to fail unnecessarily if errno has been set to a failure from any other unrelated cause.
- On iOS, Xal built with assertions enabled even in retail builds.
- On iOS, depending on how the calling app set up their work loop, it was possible for Xal to become unresponsive, particularly due to network inconsistency.
- Fixed an issue where roughly 0.8% of app installs on Android would crash on launch.
- Fixed an issue where SISU customizations do not get loaded for welcome back flows.
- Fixed a bug where UI could be shown when a silent call is made.


#### XSAPI Fixes

- Fixed an issue where deadlock could happen in the telemetry module.


### XAL Breaking Changes for all platforms

Xal has taken on the following API layer breaking changes based on API review feedback:
- `DuplicateAsyncQueueHandle()` has changed its signature. Instead of taking in a single queue handle and having that handle's reference count incremented by 1, `DuplicateAsyncQueueHandle()` now takes two arguments:
    - The first argument is the `async_queue_handle_t` you want to duplicate.
    - The second argument is of type `async_queue_handle_t*` which is used as an out param and returns a new handle which you can then reference. The new handle still needs to be closed by calling `CloseAsyncQueue()`.
    - The return value for `DuplicateAsyncQueueHandle()` has changed from being the duplicated handle to an HRESULT.
- `XalUserDuplicateHandle()` has had the same type of change done to it that `DuplicateAsyncQueueHandle()` has. Instead of taking in a single user handle and having that handle's reference count incremented by 1, `XalUserDuplicateHandle()` now takes two arguments:
    - The first argument is the `xal_user_handle_t` you want to duplicate.
    - The second argument is of type `xal_user_handle_t*` which is used as an out param and returns a new handle which you can then reference. The new handle still needs to be closed by calling `XalUserCloseHandle()`.
    - The return value for `XalUserDuplicateHandle()` has changed from being the duplicated handle to an HRESULT.
- `XalTryAddFirstUserSilentlyAsync()` has been renamed to `XalTryAddDefaultUserSilentlyAsync()`. Its functionality has stayed the same.
- The values of the enum `XalGamerPictureSize` have been changed.
- The values of the enum `XalUserChangeType` have been changed.
- The non-implemented `XalUserGetAccentColor()` stub has been removed.
- The non-implemented `XalUserCheckPrivilegesWithUiAsync()` stub has been removed and replaced with a non-implemented `XalUserResolveUserPrivilegeWithUiAsync()` stub.
- `XalUserUnregisterChangeEventHandler()` now returns `void`.
- The queue handles passed into Xal's event handlers and initialize method are no longer optional.


<!-- ********************************************************************** -->
___
## September 2018

Developers can now use XAL and XSAPI on Android and iOS platforms.


<!-- ********************************************************************** -->
___
## June 2018

### Xbox Live Features

#### C API layer for XSAPI

C APIs are now available for some Xbox Live features. The new API layer provides a number of benefits for the supported features, including custom memory management, manual thread management for asynchronous tasks, and a new HTTP library.

For more information, see [XSAPI C overview](../../api-ref/xsapi/live-xsapi-flat-c.md).


<!-- ********************************************************************** -->
___
## August 2017

### Xbox Live features

#### In-Game clubs

Developers can now create "in-game clubs". In-game clubs differ from standard Xbox clubs in that they are fully customizable by a developer and can be used both inside and outside of the game. As a game developer, you can use them to quickly build any type of persistent group scenarios inside your games such as teams, clans, squads, guilds, etc. that match your unique requirements.

Xbox live members can access in-game clubs outside of your game across any Xbox experience to stay connected to each other and to your game by using club features like chat, feed, LFG, and Mixer freely on Xbox console, PC, or iOS/Android devices.

APIs are available to create & manage in-game clubs directly from within your game. These APIs exist in the `xbox::services::clubs` namespace.


<!-- ********************************************************************** -->
___
## July 2017

### Xbox Live features


#### Multiplayer updates

Querying activity handles and search handles now includes the custom session properties in the response.

#### Tournaments

New APIs have been added to support tournaments. You can now use the `xbox::services::tournaments::tournament_service` class to access the tournaments service from your title.
These new tournament APIs enable the following scenarios:
* Query the service to find all existing tournaments for the current title.
* Retrieve details about a tournament from the service.
* Query the service to retrieve a list of teams for a tournament.
* Retrieve details about the teams for a tournament from the service.
* Track changes to tournaments and teams by using Real Time Activity (RTA) subscriptions.


<!-- ********************************************************************** -->
___
## June 2017


### Xbox Live features


#### Game Chat 2

An updated and improved version of Game Chat is now available.  See [Game Chat overview](../../features/multiplayer/chat/live-game-chat-2-overview.md).


### Xbox Live tools


#### Xbox Live PowerShell Module

* PowerShell modules have been added to make it easier to switch sandboxes on your development machine. See [Development tools for Xbox Live](../../test-release/tools/live-tools.md).


#### Bug fixes

* Various bug fixes. Check the [GitHub commit history](https://github.com/Microsoft/xbox-live-api/commits/master) for a full list.


<!-- ********************************************************************** -->
___
## May 2017

### Xbox Services APIs

#### Multiplayer

* Querying search handles now includes the custom session properties in the response.

#### Bug fixes

* Fixed "bad json" being returned instead of a valid HTTP error code.


<!-- ********************************************************************** -->
___
## April 2017

### Xbox Services APIs

#### Visual Studio 2017

The Xbox Live APIs have been updated to support Visual Studio 2017, for both Universal Windows Platform (UWP) and Xbox One (or later) titles.

#### Tournaments

New APIs have been added to support tournaments. You can now use the `xbox::services::tournaments::tournament_service` class to access the tournaments service from your title.

These new tournament APIs enable the following scenarios:

* Query the service to find all existing tournaments for the current title.
* Retrieve details about a tournament from the service.
* Query the service to retrieve a list of teams for a tournament.
* Retrieve details about the teams for a tournament from the service.
* Track changes to tournaments and teams by using Real Time Activity (RTA) subscriptions.


<!-- ********************************************************************** -->
___
## March 2017

### Xbox Services API

#### Title-managed Player Data

We have introduced a simplified Stats API.  Traditionally you had to send events corresponding to stat rules defined at Partner Center and these would update the stat values in the cloud.  We refer to this model as _event-based Stats_.

With _title-managed Stats_, your title is in control of your stat values.  You simply call an API with the most recent stat value, and that gets sent to the service directly without the need for events.  This uses the new `StatsManager` API. See [Title-managed Stats overview](../../features/player-data/stats-leaderboards/title-managed/live-stats-tm-overview.md).


#### GitHub

Xbox Live API (XSAPI) is now available on GitHub, in the <a href="https://github.com/Microsoft/xbox-live-api" target="_blank">xbox-live-api &#11008;</a> repo.

Using the binaries that come with the XDK or as NuGet packages is still recommended, however you are welcome to use the source and we welcome source code contributions.  


### Xbox Live Creators Program

The Xbox Live Creators Program is a developer program offering a subset of Xbox Live functionality to a broader developer audience.  If you are already in the Managed Partners Program, this will not have any impact on you.

See [Choosing an Xbox Live developer program](../../get-started/join-dev-program/live-dev-program-overview.md).


### Documentation

There are the following revised or new articles.

| Article | Description |
|---------|-------------|
| [Xbox Live service configuration IDs, for Managed Partners](../../test-release/portal-config/live-service-config-ids-mp.md) | Updated information on doing service configuration for your Xbox Live Title. |
| [Configuring Xbox Live in Unity](../../get-started/setup-ide/creators/unity-win10/live-configure-xbl-in-unity.md) | New information on Unity setup for Xbox Live Creators Program developers. |
| [Xbox Live Sandboxes overview](../../test-release/sandboxes/live-setup-sandbox.md) | A simplified guide to Xbox Live sandboxes and content isolation. |
| [Xbox Live test accounts](../../test-release/test-accounts/live-test-accounts.md) | Information about how test accounts work, and how to create them on Partner Center. |
