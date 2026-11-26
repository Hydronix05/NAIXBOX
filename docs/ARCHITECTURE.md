# NAIXBOX Architecture

This document describes the implementation in the current `index.html` snapshot.

## Runtime shape

NAIXBOX is currently a single HTML document containing:
- HTML elements for the loading screen, menu, HUD, hotbar, inventory, touch controls, and error overlay
- CSS for the dark interface and responsive touch layout
- A small classic script for loading progress and global error reporting
- A JavaScript module that imports Three.js and defines the game systems

Three.js 0.160.0 is imported from unpkg at runtime.

## Main systems

### Configuration and blocks

A defaults object defines world, player, graphics, and app settings. A block registry maps numeric IDs to block definitions, including display names, solidity, transparency, breakability, and colours.

The current non-air blocks are stone, grass, dirt, wood, and leaves.

### Terrain generation

Terrain is generated deterministically from a numeric seed. The height function combines several scales of smoothed 2D value noise. A grid-based tree generator places simple trunks and leaf canopies.

The terrain constants currently include sea level 8, hill amplitude 6, and dirt depth 3. The terrain generator has a version constant so future generation changes can be tracked.

### Chunks and world

Chunks are 16 blocks wide and 16 blocks deep, with the configured world height of 64. Each chunk stores block IDs in a `Uint8Array`.

The world tracks loaded chunks, pending chunk creation, and chunks that need their geometry rebuilt. Work is budgeted across frames to avoid creating and rebuilding every chunk in one update.

Chunk meshes are built from visible block faces and use vertex colours.

### Player and physics

The player uses a first-person camera controller. Movement is calculated from directional input and player yaw. The physics system applies gravity, jumping, and axis-by-axis collision checks against solid blocks.

The player is spawned near block coordinate (8, 8).

### Input and interaction

The input system supports:
- Keyboard movement and hotbar selection
- Mouse pointer-lock look and mouse-button block actions
- Touch joystick movement and right-side look gestures
- Touch buttons for jumping, breaking, and placing

The interaction system raycasts from the camera to find a targeted block within a reach of six world units. It displays a simple outline around the target.

### Inventory and game state

The inventory contains ten hotbar slots and 36 additional slots. The initial hotbar is populated with the five current placeable block types.

The game object coordinates loading, menu, playing, paused, and error states, and connects the engine, player, input, inventory, and interaction systems.

## Performance choices

The current renderer uses:
- Antialiasing disabled
- `powerPreference: "low-power"`
- A device pixel ratio cap of 1.5
- A limited number of chunk creations and geometry rebuilds per frame

These are initial choices, not a guarantee of smooth performance on every device.

## Current boundaries

The Settings button is still a placeholder. The current snapshot does not implement persistent world saves or a full settings editor. Keep documentation aligned with actual code as these systems are developed.
