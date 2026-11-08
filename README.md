# Fluid Simulation

A real-time, GPU-accelerated 2D fluid simulator built to run smoothly in a phone browser.

- **Method:** Jos Stam's *Stable Fluids* (semi-Lagrangian advection, Jacobi pressure solve, projection) plus vorticity confinement, all in WebGL2 fragment shaders with half-float textures.
- **Settings:** the Settings button opens sliders for swirliness, damping, dye fade, pressure, brush size, stir force, dye amount, render scale and resolution (with an auto toggle). Values persist in localStorage.
- **Input:** touch (multi-finger), mouse, optional device tilt (gravity).
- **Adaptive quality:** the sim/dye resolution and pressure iterations scale up and down automatically to hold ~60 fps; the HUD shows the current fps and grid sizes.
- **No build step, no dependencies:** it's a single `index.html`.

## Run

    python3 -m http.server 8000

Open `http://<your-computer-ip>:8000` on your phone (same Wi-Fi). Tilt needs HTTPS on iOS/Android, so use something like GitHub Pages or a tunnel for that button.

Requires WebGL2 + float render targets (all current iOS/Android browsers).
