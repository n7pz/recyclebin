---
title: 'Carbon Combat: Initial network & backend findings'
description: 'First findings looking onto Carbon Combat'
pubDate: 'Oct 18 2026'
heroImage: '../../assets/ccwriteup1.png'
pinned: false
---

### Context

Carbon Combat was a Unity3D game back in 2011-2012, had its own backend, used photon engine's multiplayer core and allowed for map sharing and viceversa. Eventually all of this was sunset and the dependencies the game used started deprecating.

I've been meaning to take a look onto the game for a *possible* rewrite of a backend in a mid-long term future, so I had to start by taking a look at the game's files.

Here's the hierarchy of the playable, repackaged .exe made by goutbi:

```
│   Carbon Combat.exe
│
└───Carbon Combat_Data
    │   level0
    │   level1
    │   level2
    │   level3
    │   level4
    │   level5
    │   level6
    │   level7
    │   level8
    │   level9
    │   mainData
    │   mainData.bak
    │   output_log.txt
    │   resources.assets
    │   sharedassets0.assets
    │   sharedassets1.assets
    │   sharedassets10.assets
    │   sharedassets2.assets
    │   sharedassets3.assets
    │   sharedassets4.assets
    │   sharedassets5.assets
    │   sharedassets6.assets
    │   sharedassets7.assets
    │   sharedassets8.assets
    │   sharedassets9.assets
    │
    ├───Managed
    │       Assembly-CSharp-firstpass.dll
    │       Assembly-CSharp.dll
    │       Assembly-UnityScript-firstpass.dll
    │       Assembly-UnityScript.dll
    │       Boo.Lang.dll
    │       Ionic.Zlib.dll
    │       mscorlib.dll
    │       Photon3Unity3D.dll
    │       System.Core.dll
    │       System.dll
    │       System.Xml.dll
    │       TerrainControllerData.dll
    │       UnityEngine.dll
    │       UnityScript.Lang.dll
    │
    ├───Mono
    │   │   mono.dll
    │   │
    │   └───etc
    │       └───mono
    │           │   browscap.ini
    │           │   config
    │           │
    │           ├───1.0
    │           │       DefaultWsdlHelpGenerator.aspx
    │           │       machine.config
    │           │
    │           ├───2.0
    │           │   │   DefaultWsdlHelpGenerator.aspx
    │           │   │   machine.config
    │           │   │   settings.map
    │           │   │   web.config
    │           │   │
    │           │   └───Browsers
    │           │           Compat.browser
    │           │
    │           └───mconfig
    │                   config.xml
    │
    └───Resources
            unity default resources
```

**disregard the output txt**


Initially used dnSpy to take a look to the assembly files but it was being too heavy so I decided to parse the folder to AssetRipper

long story short, here's everything involving **backend** that was accessible inside Assembly-UnityScript.dll:

## Backend

- Main address (hardcoded and found approximately 35 times): http://72.14.184.180 (No snapshots available, address was later released and used for a multiplayer MC mod 'MineZ')

#### Endpoints

##### Auth

- login.php? 
- Register.php?
- Checker.php?
- serverKeyGen.php?
- username=

##### Custom maps

- listWorlds.php?1=1
- ?search=
- ?start=
- Worlds/
- worldRating.php?
- query=...
- creator.php

##### Leaderboard and social stuff

- rankingsManager.php?request= with parameters "submit, returnMyRank, returnMyRankRel, returnUsersFromRank, returnspecific, addFriend, removeFriend and returnFriends"

##### Kongregate payments (probably for purchasing currency)

- kredsPost.php?gauth=

##### Other server side query strings

- &request=getinventoryNew&serverkey=
- &request=getrenttableNew&serverkey=


### Other domains

- dl.dropbox.com/u/4704910/CarbonCombatVersion.txt & WhirldList.txt - Was a version check and world list, no snapshots. Long gone since dropbox did a fuck all years ago.
- play.carbontechsoftware.com - Former official site
- map.syn3h.com and papawheely.com for custom map hosting. **gitea.moe** is also an option that works currently. Former mentioned URLs are dead
- i.minus.com - Holding map thumbnails, defunct.
- ge.tt/api/1/files/7i8kc5U/1..5/blob - Held music in .ogg's. Defunct
- playsmart123.appspot.com/playsmartAppEngine/relay - Looks like leftovers, no idea what it is, the base appspot url is still accessible anyways
- 4.bp.blogspot.com/…CarbonCombatTinyIcon.png - Probably icon image
- bit.ly/CCForum - Link shortener to former game forums

There also was a contact hotmail and suspicious constants involving a ""secret"" key and hashkey and serverkey handling. These are used in the auth handshake

## Current game connection

With the current .exe it's possible to connect to free, hardly stable photon servers (allegedly), with wireshark I captured the following:

- Server address: 5.8.93.52
- (If im correct) Master Server port (lobby): 5055 UDP
- Ingame port: 5056 UDP
- Photon cloud app (hardcoded): app-us.exitgames.com | Uses Photon PUN 1

## Other stuff 

The game files have Playtomic and Lumos API's and libs; Playtomic is 100% **unused**. In fact, I had to remove any files referencing it to make the unity project compile.

The game utilizes MD5 hashing. It's 2026 so yikes..

## Current progress

**Right now:** Got a compilable version of AssetRipper's exported project after a whole morning fixing errors in batch with misreferenced chars, strings, duplicated assemblyinfo, etc. State of the game is **very buggy**; some scenes are accessible, i can go from a level scene -> menu -> guest -> back in a game.

#### It's a hot mess sadly

<p align="center">
    <img src="/recyclebin/images/referencemedia/cc1.png">
</p>
<p align="center">
    <img src="/recyclebin/images/referencemedia/cc2.png">
</p>
<p align="center">
    <img src="/recyclebin/images/referencemedia/cc3.png">
</p>

Car model is CROOKED. Can't move either, can shoot though. Lots of errors come fresh from the oven and the game runs like shit (but im assuming Unity 3 is just like that)

## Next up

Fix the game to return to a playable state, preferably identical to the compiled .exe. After that, I'll come back with another update write-up. Then I will spend a long time analyzing the assemblies (Also have to learn CSharp, PHP and probably beg AI to help with UnityScript). Then migrate assemblies to modern engines along w the game (if possible) and yada yada yada

Will update when I have something new to bring


See you soon! 

~ N
