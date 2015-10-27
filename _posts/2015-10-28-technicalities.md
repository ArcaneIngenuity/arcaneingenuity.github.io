---
layout: post
title: Technicalities...
---

I'm [Arcane Engineer](http://gamedev.stackexchange.com/users/5473/arcane-engineer), some may know me from gamedev.SE where I'm no. 12 out of 55000 users... I like to think I'm qualified if not as hot as some of the other hotshots ;) Procedural generation is a major focus of mine. For those not familiar with the term, it means automatic generation of environments as found in games like Diablo, Minecraft, XCom, Moria etc. I work in C and OpenGL to provide maximum control and responsiveness.

[Arc](https://github.com/ArcaneIngenuity/arc) is the basis for WA - an open source framework I've written over the last few years which eases the process of game development while keeping us close to the metal. Arc and WA are written in C, a low level language, because portability and high performance are key, the latter not only for playability reasons, but because the game is something that will see ongoing development, we want every ounce of CPU available for later features use, including on mobiles where possible. Game architecture is another big interest of mine so I'll touch on this topic again as time rolls on.

[Orb](https://github.com/ArcaneIngenuity/orb) is another aspect that's gone into WA's development so far - it is a small, cross-platform renderer written in C/OpenGL. I thought I'd open the source in case other developers are interested or wish to make suggestions. It's geared towards OpenGL ES 2.0, which runs on mobile and on desktop under an OpenGL 4+ context. It's simple, reflecting W&A's visual style.