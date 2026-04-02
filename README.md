[![PyTorch](https://img.shields.io/badge/PyTorch-v2.0-orange)](https://pytorch.org/) [![Python](https://img.shields.io/badge/Python-3.10-blue)](https://python.org/)

SpectralCore

Minimal spectral PDE engine (~50 lines).
Drop-in 3D periodic pseudo-spectral time-stepper built on PyTorch.

⸻

What is SpectralCore?

SpectralCore is a compact 3D periodic pseudo-spectral time-stepper built on PyTorch’s rfftn/irfftn.

It provides:
	•	One-time init(grid) to precompute wavenumbers and a 2/3 dealiasing mask
	•	A single step(fields, dt, physics=None) function
	•	A pluggable physics(hats) hook for defining dynamics directly in Fourier space

The core pipeline:
	1.	Real → spectral transform (rfftn, orthonormal)
	2.	User-defined RHS in Fourier space
	3.	Explicit time step + dealiasing
	4.	Spectral → real transform (irfftn)

Supports scalar fields, multi-channel tensors, and lists of fields.
Runs on CPU or CUDA with only PyTorch as a dependency.

⸻

Capabilities

Because the physics is defined in Fourier space, SpectralCore enables:
	•	Exact derivatives via multiplication (i k, -k²)
	•	Fast Laplacians and diffusion operators
	•	Custom dispersion relations
	•	Nonlinear coupling between fields

Typical use cases:
	•	Nonlinear PDEs (reaction–diffusion, wave equations, Schrödinger-type systems)
	•	Pseudo-spectral fluid experiments (e.g., Navier–Stokes prototypes)
	•	Field simulations and pattern formation
	•	Procedural 3D fields and volumetric effects
	•	General spectral prototyping

The implementation is compact but expressive, making it useful for both experimentation and lightweight simulation workflows.

⸻

Performance & Scaling
	•	Runs on CPU (including low-power devices)
	•	Supports CUDA acceleration via PyTorch
	•	Efficient real FFTs (rfftn) reduce memory usage

Tested across a range of grid sizes, from small CPU runs to large 3D grids (e.g., 4096³ on appropriate hardware).

Quick start

import torch
from SpectralCore import init, step, laplacian

Initialize grid
init(grid=256)

Example physics: simple diffusion
def physics(hats):
    return laplacian(hats)

Create field
field = torch.randn(256,256,256)

Time evolution
for _ in range(1000):
    field = step(field, dt=0.005, physics=physics)

Why SpectralCore?

SpectralCore focuses on:
	•	Minimal implementation
	•	Clear separation of engine and physics
	•	Fast iteration for spectral methods

It is not a full simulation framework — it’s a compact core for building one.

⸻

License

MIT — do whatever you want.

⸻

Made by Rooster Murphy.
Contributions welcome.

If you would like to contribute Or buy me a coffee:

[![Buy Me a Coffee](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://paypal.me/rhouse84)

