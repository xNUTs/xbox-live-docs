---
title: Matchmaking overview
description: The SmartMatch matchmaking service selects compatible players in a multiplayer game.
kindex: Matchmaking overview
kindex: SmartMatch
ms.topic: overview
ms.prod: gaming
ms.technology: xboxlive
ms.assetid: ba0c1ecb-e928-4e86-9162-8cb456b697ff
ms.localizationpriority: medium
ms.date: 04/04/2017
---




# Matchmaking overview


## Introduction to SmartMatch

Xbox Live provides a matchmaking service, called _SmartMatch_.
SmartMatch groups players based on user information and the matchmaking request for the users who want to play together.
Matchmaking is server-based, meaning that users provide a request to the service, and they are later notified when a match is found.

There are several API approaches you can use for SmartMatch matchmaking:
* The SmartMatch matchmaking service is wrapped by [Multiplayer Manager (MPM)](../mpm/live-multiplayer-manager-nav.md).
* Or, for advanced API usage, you can directly call methods of the **MatchmakingService Class**.

If you have a matchmaking scenario that isn't supported by Multiplayer Manager, please provide feedback to us via your Microsoft Representative.
Regardless of which API you use, the conceptual information in this article applies.

When building a title, you can use SmartMatch as described in this article.
Alternatively, you can your own matchmaking service as described in [using your own matchmaking service](https://developer.microsoft.com/games/xbox/docs/xboxlive/xbox-live-partners/multiplayer-and-networking/using-your-own-matchmaking-service).
Accessing the above link requires that you have a [Partner Center](https://partner.microsoft.com/dashboard) account which is enabled for Xbox Live development.


### About SmartMatch

The SmartMatch matchmaking service works closely with Multiplayer Session Directory (MPSD) to simplify matchmaking.
SmartMatch allows titles to easily do matchmaking in the background, for example while the user is playing single-player within the title.

Individuals or groups that want to enter matchmaking create a match ticket session, then request the matchmaking service to find other players with whom to set up a match.
This results in the creation of a temporary "match ticket" residing within the matchmaking service for a period of time.

The matchmaking service chooses sessions to play together based on configuration, statistics stored for each player, and any additional information given at the time of the match request.
The service then creates a match target session that contains all players who have been matched, and notifies the users' titles of the match.

When the target session is ready, titles perform QoS checks to confirm that the group can play together, and then begin play if all is well.
During the QoS process and matchmade game play, titles keep the session state up to date within MPSD, and they receive notifications from MPSD about changes to the session.
Such changes include users coming and going, and changes to the session arbiter.


### Match Ticket Session

A match ticket session represents the clients for the players who want to make a match.
It is created based on a game, or on a group of strangers who are in a lobby together, or on other title-specific groupings of players.
In some cases, the ticket session might be a game session already in progress that is looking for more players.


### Match Ticket

Submitting a ticket session to matchmaking results in the creation of a match ticket that tracks the matchmaking attempt.
Attributes in the ticket, for example, game map or player level, along with attributes of the players in the ticket session, are used to determine the match.


## Hoppers

Hoppers are logical places where match tickets are collected.
Only tickets within the same hopper can be matched.

A title can have multiple hoppers.
For example, a title might create one hopper for which player skill is the most important item for matching.
It might use another hopper in which players are only matched if they have purchased the same downloadable content.


### Hopper Rules

Hopper rules provide definitions of the criteria that the matchmaking service uses for deciding on the players to group together.

There are two types of rules:
- MUST rules -- have to be satisfied for match tickets to be considered compatible.
- SHOULD rules -- a match ticket matching a rule is favored over one that does not.

Within each of these categories, there are several specific types of rules.
For more information, see runtime operation configuration information in **SmartMatch Runtime Operations**.


### Hopper Configuration

See the section [Basic Hopper Configuration for Matchmaking](config/live-matchmaking-config.md#hop) in the article "Matchmaking portal configuration".


### Match Target Session

Once a matched group has been found, the service creates a match target session and reserves places for all the players from the ticket sessions that are matched together.
See [Target session initialization and QoS](concepts/live-matchmaking-target-session.md).


## See also

* [Multiplayer session templates](../mpsd/concepts/live-session-templates.md)
* [Multiplayer Session Directory overview](../mpsd/live-mpsd-overview.md)
