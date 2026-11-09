# Fluid Simulation

A real-time, GPU-accelerated 2D fluid simulator built to run smoothly in a phone browser.

- **Modes:** *Water* (default) is a body of water in a box: gravity pulls it down, you can stir and splash it, press and hold to grow a water ball and release to drop it in, and tilt the phone to slosh it around. *Dye* is the original coloured-smoke mode. Switch with the Mode button.
- **Water algorithms** (Settings → Water algorithm): *Grid* is the GPU two-phase solver (water vs. air densities, very smooth, cheap on the CPU). *FLIP* is particles + a grid solved on the CPU (volume is conserved exactly and it splashes without smearing, but cost grows with the particle count; the resolution auto-adjust lowers the particle count on slow devices). Switching refills the tank.
- **Method:** Jos Stam's *Stable Fluids* (semi-Lagrangian advection, projection, vorticity confinement) in WebGL2 fragment shaders with half-float textures. Water mode is a separate solver: a staggered (MAC) grid with a two-phase water/air pressure projection (variable density, multigrid V-cycles), an advected fill-fraction field for the surface and a GPU volume-conservation step so the level doesn't drift. It is drawn with refraction, depth-based light absorption, caustics, Fresnel glints and foam.
- **Settings:** the Settings button opens sliders for swirliness, damping, dye fade, pressure, brush size, stir force, dye amount, tilt gravity strength, render scale and resolution (with an auto toggle). Values persist in localStorage.
- **Input:** touch (multi-finger), mouse, optional device tilt (gravity).
- **Adaptive quality:** the sim/dye resolution and pressure iterations scale up and down automatically to hold ~60 fps; the HUD shows the current fps and grid sizes.
- **No build step, no dependencies:** it's a single `index.html`.

## Run

    python3 -m http.server 8000

Open `http://<your-computer-ip>:8000` on your phone (same Wi-Fi). Tilt needs HTTPS on iOS/Android, so use something like GitHub Pages or a tunnel for that button.

Requires WebGL2 + float render targets (all current iOS/Android browsers).
