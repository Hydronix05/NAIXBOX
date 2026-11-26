# NAIXBOX

**NAIXBOX is a lightweight browser-based voxel sandbox game developed by NAIX Studio.** Explore a procedurally generated block world, move through chunk-based terrain, and interact with the environment by breaking and placing blocks. Built with HTML, CSS, JavaScript, and Three.js, the project focuses on a simple, accessible browser experience with performance-conscious choices for lower-end devices.

- 🎮 **Play NAIXBOX:** https://naixbox.oneapp.dev/
- 🏢 **Developed by NAIX Studio:** https://naixstudio.oneapp.dev/

> **Project status:** Early prototype (version 0.1.0). Some menu items and systems are still placeholders or works in progress.

## Features in the current prototype

- Procedurally generated terrain using seeded 2D value noise
- Chunk-based world generation and mesh rebuilding
- Grass, dirt, stone, wood, and leaves blocks
- First-person movement, jumping, gravity, and collision
- Block targeting, breaking, and placement
- Ten-slot hotbar and a 36-slot inventory grid
- Keyboard/mouse controls and on-screen touch controls
- Optional numeric world seed
- FPS display and a simple loading/error overlay
- Low-power WebGL renderer configuration

## Run it

1. Clone or download this repository.
2. Open `index.html through a local static web server, or use a browser environment that serves the file over HTTP.
3. Allow the browser to load the Three.js module from the CDN.
4. Press **Play** on the main menu.

No build step or package installation is currently required. The app imports Three.js 0.160.0 from unpkg at runtime, so an internet connection is needed for that dependency.

## Controls

| Action | Keyboard / mouse | Touch |
|---|---|---|
| Move | W A S D or arrow keys | Left-side virtual joystick |
| Look around | Click the game view to capture the pointer, then move the mouse | Drag on the right side |
| Jump | Space | JUMP button |
| Break targeted block | H or left mouse button | BREAK button |
| Place selected block | E or right mouse button | PLACE button |
| Open / close inventory | Tab or I | Hotbar's more button / inventory UI |
| Select hotbar slot | 1–9, then 0 for slot 10 | Tap a hotbar slot |

The first click in desktop play is used to capture the pointer. Press Escape to release it.

## Project layout

```text
NAIXBOX/
├── index.html           # Application markup, styles, and game implementation
├── README.md            # Project overview and getting started
├── CHANGELOG.md         # Version history
├── ROADMAP.md           # Development direction
├── .gitignore           # Local/editor files excluded from Git
└── docs/
    ├── ARCHITECTURE.md  # Current code structure
    └── CONTROLS.md     # Input reference
```

The game is intentionally kept in one HTML file at this stage. The documentation describes the current implementation; it does not imply that future systems are already available.

## Technical overview

- **Rendering:** Three.js 0.160.0, loaded as an ES module from unpkg
- **World:** 16 × 16 horizontal chunks, 64-block world height, render distance of four chunks
- **Terrain:** Deterministic seeded value noise with a simple tree generator
- **Graphics:** Vertex-coloured chunk meshes, basic lighting, fog, and a capped device pixel ratio
- **Runtime:** Native browser APIs and JavaScript; no framework or bundler

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for more detail.

## Current limitations

- The Settings button is a placeholder and currently displays a “coming later” message.
- The prototype does not yet provide a save/load system for worlds or inventory.
- Three.js is fetched from a CDN rather than bundled locally.
- The project is still evolving; performance and gameplay behaviour may change between versions.

## Development

Keep changes small and test them in both desktop and touch layouts where possible. When changing world generation, preserve deterministic results for the same seed unless intentionally introducing a terrain-version change.

For controls and code responsibilities, see the files in [docs/](docs/).

## License

No open-source license has been added yet. Unless a license is added, the source remains subject to its default copyright protection.
