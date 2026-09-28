---
title: 'From Unity webgame development to being present in a npm supply chain. What even happened?'
description: 'Adding some curious context to an incident involving a npm supply chain attack'
pubDate: 'Sep 29 2026'
heroImage: '../../assets/unity2npm0.jpg'
pinned: false
---

To be completely honest with y'all I wasn't expecting for this to be my first substantial post in the website. However, since my other projects in the works to document in here are gonna take a while since I'm busy with school and such I figured I'd just talk about this here, since it has to do with a lot of things I will be dissecting on this page. Also hadn't seen anyone connect the 2 dots, so it'd be worth saying so myself.

##### Throwback to a few months ago...

It was approximately in early June 2026 when I was scrolling on Twitter and saw the following [tweet:](https://x.com/TheHackersNews/status/2061383385927586022)

<p align="center">
  <img src="/recyclebin/images/referencemedia/tweet1.png" alt="Tweet screenshot">
</p>

As the source explains, it appeared that a third party tool on GitHub distributed via npm for Android users who use OpenAI's Codex was essentially stealing credentials. Since the malicious code was distributed through the npm package people installed, this was effectively a supply chain attack.

I won't go over the entire research of the incident itself in detail, however you could read the following post by Aikido which explains the code: www.aikido.dev/blog/codex-remote-ui-steals-ai-tokens

The final conclusion though? Allegedly the developer lost access to their npm account, then made a different statement denying any credential data. Researchers questioned the explanation, I'm not gonna speculate about their intentions here though.

<p align="center">
<b>Now here's where I walk in.</b>
</p>



<br>
<br>

## Neuron activation

Here's the funny part. Researchers evidently found that the developer (friuns) had games uploaded to the Play Store. One of them being his flagship game, *Brutal Strike*. Which is meant to be some sort of iteration of Counter Strike (duh)

And here's when my neurons got activated. As soon as I saw the names "Brutal Strike" and "friuns2" in that tweet's screenshot, I immediately snapped: It was none other than one of the developers of the legacy Unity web games **TrackRacing Pursuit** and **TrackRacing Online**

You see, it might be confusing at first glance. You might be asking 'Nico you're totally geeked this person is not the same one who made the games..!'. However, TrackRacing was made by **SoulKey** , which was an alias friuns used.

There are a handful of sources to cross-check my claims from. For example, here's a few of them:e You can check the Kongregate profiles for [SoulKey](https://www.kongregate.com/en/accounts/soulkey) and [friuns](https://www.kongregate.com/en/accounts/friuns) , both accounts have both TrackRacing games played, this is already an interesting lead if you're parting off of here.

If you don't feel confident enough, I'm sure you will now, because his youtube channel is literally [this:](https://www.youtube.com/@friuns2)

<p align="center">
    <img src="/recyclebin/images/referencemedia/yt1.png">
</p>

I also found a résumé of his where he specifies he worked on the game from 2014 to 2017. However there is some of his contact info there and I don't really feel like facilitating the access to it directly thru here. It is public though.

With the pretty obvious and straightforward confirmation there, we can move on onto the 2nd interesting topic: **the games.**


## About TrackRacing

There were a total of 2 games made by SoulKey under this name: TrackRacing Pursuit and TrackRacing Online. I will talk about both of these in release order. The first game released was TRP. Also worth noting that both games had android versions (and still have, however I will explain further later on)

### TrackRacing Pursuit

TRP is essentially based in [Edy's Vehicle Physics](https://www.edy.es/dev/vehicle-physics/). You can already notice this by the map alone and how the cars move and feel. Over this base there are several distinct car models; gamemodes and extra assets (some of which were reskinned assets from TrackMania). The game consisted majoritarily of Cops and Criminals, Races, and a deathmatch with weapons attached to your car. Also used some of Quake and TrackMania's sound effects, quite the asset party if you ask me lmao.

<p align="center">
    <img src="/recyclebin/images/referencemedia/trp1.png">
</p>

You can see some gameplay in here: https://www.youtube.com/watch?v=enO_rE9RJ0U / There's also lots of gameplay videos.


This was basically the major part of the game; you join a server (with an ancient scroll looking ui), join a game, play whatever gamemode and thats really it.

### TrackRacing Online

This one is the more juicy game out of the 2.

Not because it was a massive direct improvement of the previous one, but rather that it was headed towards being a **TMNF** browser "port", to call it like that. This lines up with what was stated earlier about the developer doing several replicas of other games for web and mobile.

This game was surely not obscure by any means back in the 2010s. TRO amassed millions of plays across several webgame portals and even was available on Facebook Gaming. Not a joke.

<p align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/zYDx9twdcrQ?si=sBw3br2aqBUdk8Ja" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</p>

There were also other modes from TRP such as deathmatch and a CTF mode, along with some extra ones I may be missing. This game also had a replay/ghost system which was all over the place, meaning you could have 20 ghosts on the track along with you. And also real multiplayer, of course.

As you may have also noticed, lots of TrackMania assets all over the place.

And I can't forgetting that as tradition in nearly all TM games, this game also had its own track editor and player-made tracks, which was nearly the entire gameplay loop of the game.

<p align="center">
    <img src="/recyclebin/images/referencemedia/trackeditor0.png" alt="Track editor">
</p>

It also had strikingly identical recreations of TMNF campaign maps made by a handful of players, all made using TMNF's assets, which were in game by that time.

<p align="center">
    <img src="/recyclebin/images/referencemedia/ao1.png">
</p>

While the latter is absolutely interesting and even funny, this rises another plausible concern.

## Withdrawals with Nadeo?

Obviously a game using assets from TM and being quite popular as a browser game was gonna attract many people's attention.

However before that, for what I've been able to find, it could have been plausible that Nadeo (TrackMania's developer studio) already found out about the game.

While whether there was a heads up on behalf of Nadeo towards the developer or not is unknown, however SoulKey decided to remove *majority* the assets pertaining to TMNF anyway (I say majority because even as of now there's still loads of stuff that belongs to TM, just reskinned). So I have 2 possible theories here:

- The developer didn't want to face legal trouble and removed the assets before Nadeo figured out
- Nadeo caught the developer and had to remove the assets either way

**Personally, I'm more inclined to believe the first option is what happened.**

I made some quick comparison image to show the before and after: 

<p align="center">
    <img src="/recyclebin/images/referencemedia/trocomparison.png">
</p>

This kinda reaffirms what I said earlier about reskinned assets. But if they have been able to keep them for over a decade guess they weren't slimed out lol


## TM players catch up

This one is particularly funny. A few years ago, several trackmania players including huge content creators found out about the game's existence.

Their representation of TRO? A mobile trackmania copy, which isn't really a lie, you get what the game shows to be.....

It's specially funny because TM players who had never heard of the game were so oblivious to the precedents of this game when they found it, which in itself is innocuous really. I personally found it hilarious when I saw their reaction myself. Let the videos speak for themselves.

<p align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/2wKWpvTl9-4?si=fYonfgfJFXXwhfGa" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>
<iframe width="560" height="315" src="https://www.youtube.com/embed/oPgcPkNjejI?si=ME8IRCZGgTqEt7JG&amp;start=387" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</p>


## How is the game doing?

To be fair, I can't say it's LIVIN LAVISH!!! But it is still playable.

It has been a few years since I last played it myself (and dare I say i lost the account I had)
In that timespan it appeared that the person maintaining the game after SoulKey's work (31416) also left development, and for whatever reasons the previous build of the game was pulled from the play store, just like TRP.


However, another member of the community took their place and is now in charge of maintaining both games. By the looks of it, they're being frequently updated and even getting new content. Definitely much better than it being dead fully.

In fact, you can simply play the game yourself, as both of them are available in Kongregate and other platforms

https://www.kongregate.com/en/games/soulkey/trackracing-pursuit
https://www.kongregate.com/en/games/soulkey/trackracing-online-tro

### Dude, how does this date back to the initial npm security incident?

I can't really find a way to directly connect them. Sometimes as a developer you're sitting one day making some games in Unity and then another day 10 years after you're uploading AI tools to Git. Time simply goes by.

## Conclusion 

I'm gonna take 2 conclusions from here, one being that you should always be wary of your accounts - specially if you're a developer, and do audits at least once every while. Maybe that way you don't wake up to a "my npm account got hijacked" scare or see yourself being kicked in the ass in Twitter by security researchers.

The second one? It's funny how something so niche as a 2010s Unity browser port of Trackmania can be linked to a developer who ended up being present in a supply chain attack.

# Thanks for reading!

<br>
<br>

##### Some stuff before I leave

Hope you all enjoyed reading the post, this one is definitely not gonna be one of the most impressive ones but at least I wanted to deliver something to the blog. I have many more stuff coming soon, though. Expect a set of posts regarding Shockwave game reversing and some stuff about my mods when I have time. School is draining a lot of my time - Seriously.

See you soon! 

~ N
