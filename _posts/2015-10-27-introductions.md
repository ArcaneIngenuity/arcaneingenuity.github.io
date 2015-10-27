---
layout: post
title: Introductions!
---

The development of the game War & Adventure (WA) will be documented here.

The game will be a first/third person hybrid FPS/RTS/RPG (all that), with a focus on exploration and ever-changing worlds, aside from the obligatory action and explosions.

Visually, WA takes a fairly abstract approach, so if you enjoyed Damocles, Darwinia, Elite, Carrier Command, Journey, Proteus, World of Goo, Worms and the like, you will probably enjoy what is in store. I grew up in the 80's when games were by necessity more abstract than they are now, which can inspire the imagination, so I like simple, soothing visuals and unobtrusive soundtracks, and meaningful gaming experiences where possible.

Siege, exploration, amazing vistas, building, and dynamic adventures are on the cards, as well as multiplayer (later). Hope you'll stick around - to stay updated, see footer links.

Introductions & Technicalities
------------------------------

I'm [Arcane Engineer](http://gamedev.stackexchange.com/users/5473/arcane-engineer), some of you may know me from gamedev.SE where I'm no. 12 out of 55000 users... I like to think I'm qualified if not as hot as some of the other hotshots ;) Procedural generation is a major focus of mine. For those not familiar with the term, it means automatic generation of environments as found in games like Diablo, Minecraft, XCom, Moria etc. I work directly with OpenGL for graphics.

WA is being developed in [arc](https://github.com/ArcaneIngenuity/arc), an open source framework I've written over the last few years which eases the process of game development while keeping us close to the metal. Arc and WA are written in C, a low level language, because portability and high performance are key, the latter not only for playability reasons, but because the game is something I'd like to work on for a long time to come, and want every ounce of CPU available for later use on extensive features, including on mobiles where possible. Game architecture is another big interest of mine so I'll touch on this topic again as time rolls on.

Another aspect that's gone into WA's development is [orb](https://github.com/ArcaneIngenuity/orb), a small cross-platform renderer written in C/OpenGL. It wasn't originally open, but I thought I'd open the source in case other developers are interested or wish to make suggestions. For now its geared towards OpenGL ES 2.0, which runs on mobile and also on desktop under an OpenGL 4+ context. It's extremely simple, reflecting W&A's intended rendering style.