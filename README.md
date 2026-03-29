# SpectralCore-128-256-320-on-Phone 

[![PyTorch](https://img.shields.io/badge/PyTorch-v2.0-orange)](https://pytorch.org/) [![Python](https://img.shields.io/badge/Python-3.10-blue)](https://python.org/)

# SpectralCore

42-line universal spectral accelerator.  
Drop-in 3D periodic spectral time-stepper built on PyTorch. Any PDE. Phone → 4096³. Zero bloat.

---

## What is SpectralCore?

It’s a drop-in 3D periodic spectral time-stepper built on PyTorch’s rfftn/irfftn (real-input FFTs) with:

- One-time init(grid) that pre-computes wavenumber grid + 2/3-rule dealiasing mask (ortho-normalized for exact energy/Parseval preservation).
- Single step(fields, dt, physics=None) that does:
  1. Real → spectral (rfftn, norm="ortho")
  2. Optional user-supplied physics(hats) → rhs_hats (you write the entire right-hand-side in Fourier space — 1–20 lines)
  3. Explicit Euler advance + hard dealias mask in one shot
  4. Spectral → real (irfftn) with .real cleanup
- Handles scalar fields, multi-channel tensors, or lists automatically. Zero config, globals kept minimal, runs on CPU or CUDA with zero extra deps beyond torch.

That’s literally it. 42 lines. No bloat.

## What it can actually do

This is a universal spectral math juggler. Because the physics hook lives entirely in Fourier space, you get exact derivatives (* 1j * K), instant Laplacians (* -K2), projections, any dispersion relation, and nonlinear terms for any system on a periodic 3D box.

### Real-world superpowers no other 42-line engine touches:
- Any linear/nonlinear PDE — wave equations, Schrödinger/Gross-Pitaevskii, Klein-Gordon, Maxwell, reaction-diffusion (spectral diffusion is stupidly fast), Burgers/KdV-style, Kuramoto-Sivashinsky, any custom dispersion or coupling you can dream up.
- Fluid dynamics & turbulence — full pseudospectral Navier-Stokes with energy-conserving projections, dealiasing, custom forcing, and viscosity. Run production-grade 3D turbulence simulations that scale from phone to 4096³ with perfect energy spectra and no aliasing garbage.
- Multi-physics out of the box — vector fields + scalars (velocity + density + temperature + phase fields + whatever). Couple 5–10 fields and still scream.
- Procedural 3D magic — time-evolving spectral noise, animated volume textures, infinite-resolution-like smooth fields (exponential convergence), perfect for game engines (drop the real-space output straight into 3D textures for smoke, fire, water, magic FX).
- Quantum / field-theory sims — real-valued base fields but complex spectral ops let you do full complex wavefunctions, Bose-Einstein condensates, etc.
- Math monster mode — spectral integrators, Poisson solvers (via one-step inverse Laplacian), exact energy-conserving projections, filtered forcing, arbitrary-order operators. All free.
- Scalability — 128³–320³ on phone (as proven). Torch FFT scales cleanly to 4096³ on big iron before memory/FFT limits bite (rfftn already saves ~50% vs full complex).

## Quick Start

bash pip install torch 

python import torch from SpectralCore import init, step, laplacian, diffuse  # One-time setup init(grid=256)          # or 128, 320, 512, 1024, 4096...  # Your physics hook (example: Navier-Stokes turbulence) def ns_physics(hats):     uhat, vhat, what = hats[0], hats[1], hats[2]   # velocity components     # ... add nonlinear terms, pressure projection, forcing here (see examples/)     return [laplacian([uhat])[0] * 0.001, ...]     # viscosity example  # Run fields = [torch.randn(256,256,256) for _ in range(3)]   # u,v,w for t in range(1000):     fields = step(fields, dt=0.005, physics=ns_physics)     # fields[0] is now updated velocity — drop straight into your 3D texture 

Built-in one-line helpers (after init()):
- laplacian(hats) → returns -K2 * hats
- diffuse(hats, nu=0.01) → returns -nu * K2 * hats

## Why SpectralCore?

It’s stupidly more general than any “fluid solver” label.  
It’s a spectral accelerator core that turns Fourier space into a playground for any math you want to evolve in 3D — while still delivering production-grade fluid dynamics and turbulence when you want it.

Phone monster. Desktop destroyer. Game-engine ready. Research ready.  
42 lines. Yours forever. MIT.

---

## License
MIT — do whatever you want. Ship it, ship games, ship papers, ship chaos.

---

Made with love by Rooster Murphy.  
Star it if it makes your 3D project faster.

Star/fork if you simulate. Contributions welcome.

If you would like to contribute Or buy me a coffee:

[![Buy Me a Coffee](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://paypal.me/rhouse84)

## License
MIT — Do your worst.
