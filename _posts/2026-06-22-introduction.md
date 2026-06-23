---
layout: post
title: "Three Months In"
author: Brian Gamble
---

I've been playing CRPGs for a long time. Bard's Tale, Ultima III, and Questron when I was a kid. Eye of the Beholder in college. Neverwinter Nights pulled me into the 3D era.

Then Oblivion, then Skyrim, and something clicked. An open world where you step outside and just go. You find a road, you follow it, and something unexpected happens.

Corundum Engine is my attempt to build something in that tradition. A 2D isometric CRPG with an open world. My own world, my own story.

## Why Build an Engine

If the goal was just to ship a game, the right call would have been to use an existing engine. But I wanted to craft something of my own, and that meant making my own architectural decisions.

I started with SFML and SDL for rendering. They worked, but at some point I decided if I was going to build this, I should go all in. That's when I switched to GLFW and Metal.

Another decision was data-oriented design. I'd watched several talks on it and the performance benefits were hard to ignore. Object-oriented code can get complicated fast, with things hiding inside other things. Data-oriented design keeps it flat and straightforward.

Building an engine from scratch also seemed like the most interesting way to understand how games actually work. After years of web development, I was ready for a different kind of problem.

There's one more reason. Most games and engines are built for PC first, with Mac as an afterthought, if at all. I'm developing on a Mac, and I wanted native Apple Silicon support, not a port.

The game has a codename for now, Project Keystone. A keystone is the central stone of an arch that holds all the other pieces in place. It felt like the right name for the piece that brings the engine to life.

## The Beginnings

I started building the engine in March. The early version of the game used top-down sprites. A player could walk through a world made of 128×128-tile chunks, loading new areas on demand. Conversations with NPCs were already in place, with branching choices and conditions.

The tools came alongside the engine, and I built all of them from scratch. Tilesmith is a tilemap editor that outputs straightforward JSON in exactly the shape the engine expects. Spritepacker is a CLI tool for packing individual sprites into texture atlases. Spritesmith is a visual sprite sheet editor for defining and previewing animation clips. Worldsmith imports a fantasy map from [Azgaar's Fantasy Map Generator](https://azgaar.github.io/Fantasy-Map-Generator/), lets me paint terrain and place settlements, and exports the result as a grid of tilemap chunks. And finally, Talesmith, a node-based visual editor for dialogue graphs.

The pieces were coming together, but something wasn't right.

## The Pivot

As I walked around the test world, it looked like a map, not a place to explore. Top-down orthogonal flattens everything.

I switched to isometric and I believe it will be better. The added perspective gives the world depth that top-down can't match. You can see the sides of buildings. Elevation reads clearly. Characters feel grounded in the environment. It's not Skyrim, but it's closer to the feeling I'm after.

The switch is costing time. The tilemap format changed, the renderer had to be rewritten for isometric projection, and the camera logic needed rethinking. More changes are still needed, but I think it's worth it.

## What's Next

The immediate priority is getting world streaming working again under the isometric renderer. After that, a quest system to track objectives and story progression. Then character stats and a basic rules engine.

The road is long, but the foundation is forming.
