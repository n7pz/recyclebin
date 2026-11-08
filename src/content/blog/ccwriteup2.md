---
title: 'Updates on Carbon Combat'
description: 'Status update on my project involving Carbon Combat as of November 2026'
pubDate: 'Nov 8 2026'
heroImage: '../../assets/ccwriteup2.png'
pinned: true
---

## Hi all

Surprisingly it has been 3 weeks since I last posted in here. Unfortunately time with school caught up to me again, and I was putting my focus more on commuting between school and Carbon Combat rather than doing anything else. Would I like to have more free time back? Yes. Can I? Not yet, sadly. Anyways, since the previous post I have made **LOTS** of progress. First I would like to make some corrections from my initial findings:

**sadge disclaimer: since I had little time daily but dedicated daily sessions to it, I didn't really document with screenshots or code snippets. I will love to do it for future posts!**


#### What was wrong after the AssetRipper export?

A lot of things unsurprisingly. Let me quote some of the issues from the first post.

> Car model is CROOKED. Can’t move either, can shoot though. Lots of errors come fresh from the oven and the game runs like shit (but im assuming Unity 3 is just like that)

I'm gonna explain from simplest to hardest solutions in here.

- Couldn't move: I was a dumbass and I was supposed to enter play mode from Preloader.unity
- The game runs like shit: Placebo effect, it later worked correctly.
- Car model was crooked: This one was really tricky. As you could see in the picture I had a strange rectangle mesh on the back of the car. This was the missile launcher mesh. Apparently assetripper changed the hierarchy of the meshes inside the Cars (namely CarPrefab). MissileLauncher was inside the back left wheel. I moved it to the same spot the weapon children were


#### About textures

A known issue with AssetRipper (at least its free version) is that it is not capable of exporting shaders. Instead it utilizes a Dummy exporter which resulted in receiving malfunctional textures. Hence the gray.

Since I don't know how to restore said shaders off the get go. I was barely 2 or 3 days in and was still attempting to understand the codebase, I wasn't able to recover 1:1 the shaders myself. So I used a little bit of *magic*. And by magic I mean *sentient technological magic*. It has been of great help in the migration really, especially with keeping the game 1:1 in engine hops.

Practically all of the shaders had to be restored. Some of the most notable were:

- CarbonPaint (car shader)
- Water shaders
- Glass and transparent items

#### CarPrefab issues

This one has been the biggest headache I've had so far. 80% of the issues that had been fixed in the Unity project all came back to the prefabs of the Blue team and Red team cars respectively. Freeplay uses the red team car prefab.

Most importantly: The red team prefab had blue materials assigned. I had to reassign it to the red materials by hand and later on assign the meshes that should be bleached in freeplay to the mainmeshes section.

If this wasn't enough the hierarchy wasn't permanently fixed: The component holding PhotonView (what decides damage dealing and viceversa) was in a wrong level of hierarchy. So I spent quite a while figuring out why was I permanently godded.


#### Water wasn't watery.

The water shaders were the ones that fought against me the most: Fixed the main water shader, it was still flickering. Changed it: still flickering. Added the ripple texture in: still flickering.

The solution? The fucking transparent shader. 

And that wasn't the end of it!!

The splash effect that spawns upon the car touching water (or a rocket projectile) wasn't spawning. I also spent a while figuring out what was the issue, just for the 'Life' property of the prefab being at 0 for some reason. Put it at 1.5 and it was fixed.


**That sums up the first few days or so of fixing problems. I may be missing some stuff but I covered the most important issues by that date**


#### HOLD ON! Did you get permission to continue the project?

Yep! I emailed CarbonTech himself, explaining the progress I had made so far, what I wanted to achieve and asked for permission for the usage of the codebase and assets, along with the name. 2 days later he replied with this:^

>Hi Nico,
>
>This is neat! Yes, you have my permission to publish the code/assets and use the Carbon Combat name for the project.
>
>Best of luck,
>Andrew


After I received his word, I was fully hands-on in the project.

Since the major issues from the export had already been addressed by then, I settled in and posted the source project to Git. (You probably have seen it already if you visited my github profile, or maybe not, idk who reads these articles if any =) )

In case you haven't - Take a look at the repo. Commit history is available there: https://github.com/n7pz/CarbonCombat-source 


After this explaining what I worked is trivial: Kept fixing color assignments, have the game load mars explorer's assets for whirld loading and etc


#### Tackling legacy issues


It had been known that going out of your car in the original repackaged exe file caused crash. I was able to look onto this, and the root cause was the following: The HumanPrefab's shadow projector casted shadows infinitely, which would crash anyone on 64 bits. This mostly explains why compatibility mode as Windows 7 would help with stability.


#### Store access?

Yeah. I was able to take a peek on how the old backend was like: **chaos**

The entirety of the persistent data was saved all into a **SINGULAR TABLE**. Then the game read it with pipes separating each value, bool and integer.

Anyways, I created a table in SQLite to cover all of the data, and then I *cough* magically came up with a simple backend in CSharp that listens on localhost:5158 <br>
I also made it so you have enough cash to max out and try out all cars!

How it works: The game asks for the .php endpoint, the backend returns what the game is able to read. (like ?username=, etc)
And with that I was able to recover account-locked content.

## Next step: Our first migration

As of writing this, it's already been done! Currently I have the game fully working on Unity 5.6, and I'm positive that future migrations will also be possible.

### Unity 5 changes

Honestly I had expected it to be worse, but the major features that broke were shaders (that were gonna die out anyway) and physics. I also discovered that the game used NVIDIA's PhysX 2, now it uses PhysX 3. It's still old, but I expect it to not break as much for future hops.

The physics had to be recreated drastically: Gravity, engine torque, handling, weight reduction or augmentation on cars, boost multiplication... 

The shaders were also recreated accordingly. Fortunately the magenta color is not living rent free in my head.
Whirlds unfortunately aren't supported anymore, but I will make sure they're back along with .dae loading (WHICH WORKS IN UNITY 3.5 BTW)

<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/QoHcpNs9oRM?si=XS5FunCDwFDSdmsp" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></p>

I also made sounds point to a local file:// path instead of ge.tt, unfortunately original sounds were dead, so I just downloaded and edited a rain, waterfall and underwater sound.


### Pretty cool teaser

I also made a teaser for the game. I duplicated the project and made a director tool that made the car drive forward in a dark environment, then get shot by a rocket and fade to black. I also have made an initial draft of the logo I want to use for the project. It's not definitive (and I find it ugly)

<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/8cOjeH-BKPs?si=X1AnNfeFxy4LBXno" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></p>


## I wanna play!!

Currently I have 2 builds ready: the Unity 5 build and the 3.5 one with whirld support (the latter isn't fully updated because the team colors weren't 1:1)

Anyhow, if you wanna play, since both have the backend working, here are the links:

**Unity 5** - https://rinna.s-ul.eu/CarbonCombat/sdAOGr6k <br>
**Unity 3.5** - https://rinna.s-ul.eu/CarbonCombat/3HH8JXXg


<p align="center"> And this sums up my work for the last 3 weeks or so. </p>

<br> <br>

I hope I explained myself clearly, and that whoever reads this feels positive about the project, just like I am.
About the next update post... I don't know when. Exams are around the corner, school is draining me and mood swings hit me hard where sometimes I have days I am completely pissed off and unproductive. Perhaps next one will be once I end the Unity 2017 migration, but expect it to be by the end of November.

<br>

See you soon!

~ N