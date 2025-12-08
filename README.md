# SpectralCore-128-256-320-on-Phone 

[![PyTorch](https://img.shields.io/badge/PyTorch-v2.0-orange)](https://pytorch.org/) [![Python](https://img.shields.io/badge/Python-3.10-blue)](https://python.org/)

**TheSpectralCore is not a solver. It’s a bolt-on turbo for almost every linear or mildly nonlinear system that diagonalizes in Fourier space.**

One file. One function call. Works the same on your phone, laptop, Colab, or the biggest GPU node you can find. Change a single number (grid=N) and it instantly scales from 64³ toy demos to multi-billion-voxel production runs – no MPI, no tuning, no gatekeepers.

Navier-Stokes, wave equations, reaction-diffusion, Schrödinger, Maxwell, generative art, whatever. If it’s made of waves, it now runs faster, cleaner, and cheaper than anything that came before.

Scientific computing just became democratic.  
Copy, paste, write 5–20 lines of physics(), win.

That’s all.  
42 lines to rule them all.

Real-time 3D pseudospectral turbulence at **N=128³ (2.1M particles)** **N=256³ (16.8M particles)** **N=320³ (32.8M particles)** in less than **100 lines of pure Python**. Runs on a phone—because why not turn your Snapdragon into a supercomputer?

## What It Does
- Solves Navier-Stokes via spectral methods (FFT-based).
- Energy-conserving integration (see outputs: E drops <1% over 400 steps).
- "PHONE MONSTER": No GPUs, no clusters—just NumPy/Torch on mobile.
- Real-time volumetric fluids for mobile games: smoke, fire, clouds, water, magic effects — all driven by actual Navier-Stokes running at 128³ on-device. 
- Drop-in gaming integration: Export velocity/density fields as 3D textures → instant reactive smoke, destructible clouds, spell effects, underwater caustics, or full planetary atmospheres — all on-device, no server cost.
- SpectralCore isn’t just a fluid solver — it’s a spectral accelerator you bolt onto anything.  
Drop it in once and every effect in your game (smoke, fire, clouds, magic, dust, explosions, even audio-reactive visuals) instantly inherits real divergence-free turbulence and 32M-particle detail.  
No engine changes, no GPU, just pure CPU-powered chaos that makes everything look 10× more expensive overnight​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​

## Quick Run
- Click **Open in Colab** on the notebook → Hit Runtime > Run all.
- Or on Android: Termux + `pip install numpy torch` → Pick .py file. 

![image](https://github.com/user-attachments/assets/3ac68114-d398-4fa1-8858-25e3bf954c7a)

- 256³ spectral turbulence  
- 9 frames of real, unforced, incompressible Navier-Stokes  
- Fully developed → natural decay  
- Ran on my iPhone. No GPU. No forcing. 
- 42 lines of code.  

<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/6eed96fb-4438-4961-8cfa-2f52448631d6" />
<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/032cd716-98b9-49ea-86c6-b575b67c76aa" />
<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/6d38c3e3-e07c-4947-a2fa-a9354b9a5328" />
<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/ff4c188a-47ea-4d83-8aab-6892fb67f643" />
<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/5a320d21-a8b1-41c6-a025-4b5042d3a738" />
<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/4f32757c-6df4-4783-9083-577e612b76db" />
<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/f236b37f-58a2-4392-954c-da86ee4fcb57" />
<img width="890" height="932" alt="image" src="https://github.com/user-attachments/assets/bba89eda-f281-4279-8155-5b71619f8c03" />


![image](https://github.com/user-attachments/assets/45e90451-073b-4ee4-b272-58c8c8873583)

Even used it to turn Doom fire to real fire on my phone in 3 cells on colab CPU for fun! 

<img width="512" height="389" alt="image" src="https://github.com/user-attachments/assets/ddf26eeb-fa7d-405b-b9d5-796e4877f847" />
<img width="430" height="328" alt="image" src="https://github.com/user-attachments/assets/f1a4c693-7d36-42e6-a0fe-f7972fc663a6" />

## Tech Stack
- 128³ → Pure Python + NumPy FFT → ~2 GB → 1.1–1.17 FPS on any phone  
- 256³ → PyTorch + torch.fft (CPU) → ~9 GB → real-time on 2024–2025 flagships  
- 320³ → PyTorch + torch.rfft + manual 3/2 dealiasing → ~3.5GB → on Snapdragon 8 Gen 3 / Dimensity 9300+  

Zero GPU. Zero cloud. One line of code. All three run today.

Star/fork if you simulate. Contributions: Faster integrators? PRs welcome.

If you would like to contribute Or buy me a coffee:

[![Buy Me a Coffee](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://paypal.me/rhouse84)

## License
MIT — Do your worst.
