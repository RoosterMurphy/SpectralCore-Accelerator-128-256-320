# Turbulence128-on-Phone 

[![PyTorch](https://img.shields.io/badge/PyTorch-v2.0-orange)](https://pytorch.org/) [![Python](https://img.shields.io/badge/Python-3.10-blue)](https://python.org/)

Real-time 3D pseudospectral turbulence at **N=128³ (2M+ particles)** in **94 lines of pure Python**. Runs at **1.1 FPS** on a phone—because why not turn your Snapdragon into a supercomputer?

## What It Does
- Solves Navier-Stokes via spectral methods (FFT-based).
- Energy-conserving integration (see outputs: E drops <1% over 400 steps).
- "PHONE MONSTER" mode: No GPUs, no clusters—just NumPy/Torch on mobile.

## Quick Run
- Click **Open in Colab** on the notebook → Hit Runtime > Run all.
- Or on Android: Termux + `pip install numpy torch` → `python T128-on-Phone.py`.

## Outputs (from your run)
| Step | Energy (E) | FPS | Time (s) |
|------|------------|-----|----------|
| 0    | 31.006     | -   | 0.00    |
| 100  | 30.945     | 1.17| 85.8    |
| 200  | 30.828     | 1.17| 171.4   |
| 300  | 30.819     | 1.17| 256.2   |
| 400  | 30.758     | 1.17| 341.0   |

![image](https://github.com/user-attachments/assets/3ac68114-d398-4fa1-8858-25e3bf954c7a)


## Tech Stack
- **Core**: PyTorch for tensors/FFTs (falls back to NumPy).
- **Size**: 128³ grid → ~2GB RAM peak (phones handle it!).
- **Why Phone?** Proof-of-concept: High-fidelity CFD anywhere.

Star/fork if you simulate. Contributions: Faster integrators? PRs welcome.

256 and 320 in the works. If you would like to contribute Or buy me a coffee:

[![Buy Me a Coffee](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://paypal.me/rhouse84)

## License
MIT — Do your worst.
