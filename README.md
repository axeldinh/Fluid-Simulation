# Fluid Simulation

A real-time 2D water simulator built to run smoothly in a phone browser.

- **What it is:** a body of water in a tank. Gravity pulls it down; drag to stir and splash it, press and hold to grow a water ball and release to drop it in, and tilt the phone to slosh it around.
- **Water algorithms** (Settings → Water algorithm):
  - *Grid* (default): a GPU solver on a staggered (MAC) grid with a two-phase water/air pressure projection (variable density, multigrid V-cycles), an advected fill-fraction field for the surface and a GPU volume-conservation step. Very smooth and light on the CPU.
  - *FLIP*: particles carrying velocity plus a grid pressure solve, on the CPU. Volume is conserved exactly and it splashes without smearing, but cost grows with the particle count (the resolution auto-adjust lowers it on slow devices).
  - Switching refills the tank.
- **Rendering:** refraction of the back wall, depth-based light absorption, caustics, Fresnel glints and foam.
- **Settings:** gravity, water density vs air (grid), FLIP blend and pressure iterations (FLIP), ball growth speed, tilt strength, brush size, stir force, render scale, resolution level (with an auto toggle). Values persist in localStorage.
- **Input:** touch (multi-finger), mouse, optional device tilt (gravity).
- **Adaptive quality:** the simulation resolution scales up and down automatically to hold ~60 fps; the HUD shows the current fps and grid sizes.
- **No build step, no dependencies:** it's a single `index.html`.

## Run

    python3 -m http.server 8000

Open `http://<your-computer-ip>:8000` on your phone (same Wi-Fi). Tilt needs HTTPS on iOS/Android, so use something like GitHub Pages or a tunnel for that button.

Requires WebGL2 + float render targets (all current iOS/Android browsers).
