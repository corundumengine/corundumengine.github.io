---
layout: post
title: "Clearing the First Dungeon: The 0.2.0 Milestone"
author: Brian Gamble
---

Corundum Engine is still pre-alpha, so 0.2.0 is not a product release. It feels more like the first dungeon is behind me: enough of the underlying systems work together to establish a real baseline, while most of the work still lies ahead.

For me, marking a version now is about discipline and taking stock. Engine development can become open-ended churn, and a milestone forces me to describe the system as it actually exists: what works together, what remains unstable, and what needs more iteration. It also gives future changes a concrete baseline instead of a vague memory of "earlier."

## The Runtime Foundation

The runtime is coherent enough to describe as a system. Simulation runs at a fixed timestep with render interpolation, a random-number generator seeded at startup so any run can be replayed exactly, and explicit pause handling for focus loss and controller disconnect. The entity model is data-oriented, the same approach I described in [Three Months In](/blog/2026/06/22/introduction/): structure-of-arrays tables that keep the data flat, generation-counted handles that can't be mistaken for a recycled entity, and two-phase deletion that waits until a frame's updates are done.

What took the most care was drawing the lifecycle boundaries. Entity lifetime, pause state, and frame rendering each needed their own scope, so that stale entities and game-specific hooks could not collapse the whole thing back into one tangled loop.

## The Isometric Renderer and World Model

Rendering meets the world model. The renderer has Metal (macOS) and GLCore (Windows and Linux) backends, elevation-aware draw order and collision, viewport culling that skips whatever is off screen, and UTF-8 text. Above that, the engine supports both single maps and chunked worlds, including portals, spawn points, and chunk-resident actors that stream in and out with the terrain around them. The click-to-move pathfinding across walkable terrain, stairs, and ramps is in place but hasn't been exercised on a real map yet.

Isometric presentation only holds up if everything behind it agrees on where things are. Elevation, collision, and draw order have to line up, or a character sorts into the wrong depth and a path cuts through a wall. Getting them to share one representation was the real work. The test world is still open terrain, a road, and a stand of trees, though. The buildings that will actually sell the perspective are next on the list.

## The Content Pipeline

The content path extends from authoring to validation to runtime. Tilesmith, Spritesmith, and Loom cover tilemaps, sprite sheets, dialogue, quests, and items through a shared editor toolkit. Loom is the dialogue editor I first wrote about as Talesmith, grown to cover quests and items as well. The runtime loads JSON-driven content; the content formats carry schema versions, and validation runs at the editor/runtime boundary so the two sides fail loudly when the contract is wrong. Save files are versioned separately, with a migration chain that upgrades old saves as the format changes.

The formats are interfaces. Editors and the runtime drift apart over time, and the schemas are what keep that from turning into silent breakage.

There is plenty of roughness. This is not ready for other developers to build games on. APIs, file formats, and tools can change without notice, and the authoring guides are explicitly works in progress.

## What's Next

The next stretch is continued iteration on that unstable surface: testing the integrated runtime and editors, tightening contracts that do not hold up, and keeping schemas and documentation aligned as formats change. It is also time to put some real buildings and props into the world. I already have some test quests and items to try out, which means a quest UI comes next.

The one thing I've deliberately left open is combat. Character stats and a rules engine will shape everything around them, so I wanted the world, dialogue, quests, and items solid first. What combat actually looks like is still an open question.

If you want the full inventory, the [0.2.0 changelog](https://github.com/corundumengine/corundum/blob/main/CHANGELOG.md) has it.

The first dungeon is cleared and I've leveled up. The next one is deeper.
