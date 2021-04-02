---
title: "XR-045: Xbox Live and Account Privileges"
description: Titles must check whether the active user has certain privileges before completing certain actions.
kindex: "XR-045: Xbox Live and Account Privileges &diams;"
kindex: policies
ms.topic: article
ms.localizationpriority: medium
ms.date: 03/18/2019
---

# XR-045: Xbox Live and Account Privileges

Xbox Live promises users a certain level of privacy and online safety for themselves and their children. In order to deliver on that promise, titles must check whether the active user has certain privileges before completing certain actions on the Xbox Live service or in a title experience.

| **Activity** | **ID** | **Privilege Name** | **Notes** |
|-|--|--- |---|
| Playing in a multiplayer game session | 254 | XPRIVILEGE_MULTIPLAYER_SESSIONS | Allows a user to join multiplayer gameplay sessions with real-world users (not bots) in scenarios such as: Synchronous player-vs-player gameplay in the same session, asynchronous turn-based gameplay, Team-based gameplay, User-initiated matchmaking, Sending or accepting invitations, Join-in-progress sessions. |
| Playing in a cross network game play session | 185 | AuthPrivileges.CrossNetworkPlay | Allows a user to participate in a gameplay session with other real-world players who are not signed into Xbox Live in scenarios such as: Synchronous player-vs-player gameplay in the same session, asynchronous turn-based gameplay, Team-based gameplay, User-initiated matchmaking, Sending or accepting invitations, Join-in-progress sessions. |
| Communication with anyone | 252 | XPRIVILEGE_COMMUNICATIONS | Allows a user to communicate with any other Xbox Live users through voice or text. |
| Shared gaming sessions | 189 | XPRIVILEGE_SESSIONS | Allows a user to participate in connected single-player experiences in shared environments. These experiences must not have any features covered under privilege 252 or 254 (Communications and Multiplayer, respectively). Use of this privilege is a title capability that requires platform approval. |
| User-generated content (UGC) | 247 | XPRIVILEGE_USER_CREATED_CONTENT | Allows a user to see other users' UGC online, download other users' UGC, or share their own UGC online. This does not restrict usage of previously downloaded UGC. |
| Sharing to a social network | 220 | XPRIVILEGE_SOCIAL_NETWORK_SHARING | Xbox One Only: Allows a user to share information, including game progress, Kinect-generated content, game clips, and so on outside of Xbox Live. |


## More Information

If your services processes Xbox Live issued tokens, you should enforce on your service that the users in the session have the appropriate privileges to perform the requested action by inspecting the "prv" claim for those users inside the token.

If a title offers one or more of the activities listed in the above table, the title must check privileges associated with the particular activity. If a user does not have the privilege, the user must not be allowed to use the associated activity. Privileges are granted for the duration of the session/action or the time before the Xbox Live token is refreshed, whichever is shorter.


### On Windows 10

The user does not have the privilege if it is absent from the "prv" claim and the title should prevent the user from continuing with the privileged activity. If the check was triggered by the user requesting access to the privileged activity, such as trying to start or join a multiplayer session, the title should show an informative message to let them know they cannot participate. Suggested messaging is including in the privilege table above.


### Xbox Live Connectivity Issues

If the title receives a failure (either through the API or because it cannot retrieve an Xbox Live token) because the Xbox service is unreachable, the title should block access to the requested action. In such instances, the title should fail gracefully, as described in XR-074, "Loss of Connectivity to Xbox Services," located in this document.


## Recommended Test Cases


### 045-01 Respect User Privileges


#### Test Steps

1. Sign in to a profile and launch the title.

2. For each of the privileges identified in the XR, identify if the title supports the associated activity.

3. For each possible setting of each applicable privilege identified in step [2], perform the following:

    * Exit the title and change the user's settings for the privilege.

    * Restart the device.

    * Sign into the same profile and launch the title.

    * Visit all relevant areas of the title, use all title features relevant to the privilege and verify that the title respects the user's current privilege setting.  


#### Expected Result

Titles must honor the user's privilege settings.  


#### Pass Examples

1. The title respects the user's privilege settings.

2. The title treats a partial-allow privilege setting as if the privilege is disabled/disallowed.
   For example, when the User-generated content (UGC) privilege is set to **Friends Only**, the title behaves as if the privilege is set to **Blocked**.

3. For titles using the Xbox One XDK, the title invokes the system UI to alert the user of any privilege conflicts (titles must use the `Store::Product::CheckPrivilegeAsync` API).

4. For titles using XSAPI, the title shows an informative message to let the user know they cannot participate.


#### Fail Examples

1. The title persists a user's privilege settings and does not reflect the user's actual privileges after they have been changed.

2. The title treats a partial-allow privilege setting as if the privilege is set to its least restrictive setting.
   For example, when the User-generated content (UGC) privilege is set to Friends Only, the title behaves as if the privilege is set to Allowed.

3. For titles using the Xbox One XDK, the title uses in-game messaging to alert the user of any privilege conflicts and does not display the System UI.

4. For titles using XSAPI, the title does not show an informative message to let the user know they cannot participate.
