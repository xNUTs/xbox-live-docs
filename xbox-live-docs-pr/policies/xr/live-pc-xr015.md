---
title: "XR-015: Privacy and Permissions"
description: Titles must not transmit user data or allow communication over Xbox Live when the user's privacy & online safety settings do not allow it.
kindex: "XR-015: Privacy and Permissions"
ms.topic: conceptual
ms.localizationpriority: high
ms.date: 10/01/2019
---

# XR-015: Privacy and Permissions 

Titles must not transmit user data or allow communication over Xbox Live when the user's privacy settings do not allow it.

Titles meet this XR by retrieving data from Xbox Live services. If the title uses its own services, it must check the user's privacy permissions at the beginning of a session or when a new user joins the session. For user-initiated scenarios outside of sessions, titles meet this requirement by checking privacy prior to displaying the user's data and before performing the action. The following list of privacy settings is available for titles to check:


| Permission name |Description |
|-------------------|-|---------------|
|CommunicateUsingText | Check whether or not the user can send a message with text content to the target user. |
|CommunicateUsingVoice |Check whether or not the user can communicate using voice with the target user. | |

During the gameplay session, titles which offer communication between Xbox Live and non-Xbox Live network players must offer the ability to mute any non-Xbox Live players for the duration of the session.

## More Information

Prior to allowing any activity to occur, titles must also check the Xbox Live service for privileges, as stated in [XR-045: Xbox Live and Account Privileges](live-pc-xr045.md).

Titles that support cross-network play and communication between Xbox Live and non Xbox Live players need to check communication permissions prior to allowing communication between those players.  

Titles check communication settings for cross network players by using "_CrossNetworkUser_"  which acts as a replacement for the XUID (see XDK). Based on Xbox Live privacy settings, these users will return a result of "allowed" only when the Xbox Live user's permissions are set to allow communication with all cross network players. Titles which support a cross network friends list can check communication between cross network friends by using "_crossNetworkFriend_" as a replacement for the XUID.  Based on Xbox Live privacy settings, "_CrossNetworkUser_" will return a result of "allowed" only when the Xbox Live user's permissions are set to allow communication with all cross network players while _"crossNetworkFriend"_ will return 'allowed' when the Xbox Live user's permissions are set to allow communication with all or cross network friends only.

## Intent
Ensure that customers have appropriate and consistent control over their personal information.


## Implementation Guidance and Best Practices

## Additional Resources


## Certification Test Cases
**015-01 User Communication**   
  
>**Configuration:** 
>* Create a set of profiles with “Others can communicate with voice, text or invites” to Everyone, Friends and Blocked.
>* For titles that support communication outside of Xbox Live, create a set of profiles with “You can communicate outside of Xbox Live with voice & text” to Allow, In-game friends and Blocked.
>    * Note:  The difference between the “Allow” and “In-game friends” friends options are that “Allow” means you can talk to everyone cross network (including players you meet in random matchmaking). “In-game friends” are people you’ve explicitly chosen to play with by adding them to an in-game friends list.

>**Test Steps**  
>1. On Device 1, sign in to a profile that has been configured with the specific set of permissions per the Configuration.
>2. On Device 2, sign in to a profile that has no communication restrictions.
>3. On both devices, launch the title and attempt to communicate using text, voice (both via Kinect and via the headset), and video in every location supported and attempt to send game invites.
>4. Repeat Steps [1] – [3] for all profiles from the Configuration step.
>
>**Expected Result**  
>Titles must check the Xbox Live service for a user’s permissions regarding privacy and online safety-related actions and must not transmit user data or allow communication over Xbox Live when the user’s privacy & online safety settings do not allow it. 
>
>**Pass Examples**  
>1. The title prevents the user from communicating via voice and text over Xbox Live when that specific method of communication is configured to be blocked.
>2. The title prevents the user from communicating via voice and text outside of Xbox Live when that specific method of communication is configured to be blocked.
>3. The title prevents the user from receiving invites on Xbox Live when that is blocked.
>
>**Fail Examples**  
> 1. The user is able to communicate via voice and text over Xbox Live when that specific method of communication is configured to be blocked.
>2. The user is able to communicate via voice and text outside of Xbox Live when that specific method of communication is configured to be blocked.
>3. The title allows the user to receive invites on Xbox Live when that is blocked.  

<br />

**015-02 Muting Support**   
>
>**Test Steps**  
>1. As user A, mute user B.
>2. Have both users join an Xbox Live multiplayer session.
>3. Attempt to send voice communication from user B to user A.
>4. Ensure that user A is unable to receive any voice communication from user B.
>
>**Expected Result**  
>User A must not be able to hear communication from user B.  
>
>**Pass Examples**  
>1. Voice communication from the muted user cannot be heard by the user who initiated the mute.
>
>**Fail Examples**  
>1. Voice communication from the muted user can be heard by the user who initiated the mute.  
<br />

**015-03 Blocked Users**   

**Test Steps**  
>1. As user A, block user B.
>2. Have both users join an Xbox Live multiplayer session.
>3. Attempt to send voice and written communication from user B to user A.
>4. Locate any title-provided invitation mechanisms (any invitation mechanism that does not utilize the Xbox Shell).
>5. Using each of the mechanisms located in step [4], attempt to send a game invite from user B to user A.
>6. Ensure that user A is unable to receive any communication or invites from user B.

**Expected Result**  
User A must not be able to hear or see communication from user B. User A must not be able to receive game invitations from User B.  

**Pass Examples**  
> 1. Communication from the blocked user cannot be seen or heard by the user who initiated the block.  
> 2. Game invitations from the blocked user are not received by the user who initiated the block.

**Fail Examples**  
> 1. Communication from the blocked user can be seen or heard by the user who initiated the block.
> 2. Game invitations from the blocked user are received by the user who initiated the block. 
>
<br />