# 🌊 AuraPhaser: Ultimate Worklet Edition

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Web Audio API](https://img.shields.io/badge/Web_Audio_API-Enabled-success.svg)]()
[![Zero-Dependency](https://img.shields.io/badge/Dependencies-None-brightgreen.svg)]()

**AuraPhaser** is a production-grade, browser-based Digital Signal Processing (DSP) engine that transforms a live microphone input into a massive, parallel phase-shifting matrix. 

By utilizing a custom, C++ style `AudioWorkletProcessor`, AuraPhaser is capable of running **up to 20,000 concurrent All-Pass Filter chains** in real-time on a dedicated low-latency audio thread, all without crashing the browser.

---

## 📖 Overview

Standard Web Audio API nodes (`BiquadFilterNode`) are limited by the browser's main thread overhead. When chaining thousands of nodes, Garbage Collection (GC) stutters and CPU overload are inevitable. 

AuraPhaser solves this by bypassing standard Web Audio Nodes entirely. Instead, it computes audio mathematically at the sample level (1/48,000th of a second) using heavily optimized `Float32Arrays`, branchless logic, and an 8192-point Trigonometry Look-Up Table (LUT).

The result is a mesmerizing, sweeping, "jet-engine" or "underwater" phase cancellation effect that can be pushed to extreme, mathematical scales.

---

## ✨ Core Features

* 🚀 **Extreme Scale DSP Matrix:** Configure up to 20 independent "Engines," each pushing up to 1,000 parallel tracks. That's 20,000 simultaneous phase-shifted paths.
* ⚡ **Zero-Branch Worklet Architecture:** Built using raw `Float32Array` memory allocation, completely eliminating Garbage Collection (GC) stuttering.
* 🧮 **Look-Up Table (LUT) Optimization:** Bypasses heavy per-sample `tan()` calculations by pre-computing 8,192 trigonometry bounds on boot, achieving maximum CPU cache locality.
* 🔄 **"Invert Aura" Protocol:** An atomic, 1-sample command that instantly inverts the wet mix phase (180 degrees) and mathematically mirrors all active frequencies to the opposite side of the human hearing spectrum.
* 🎛 **Automated Matrix LFOs:** Generate auto-stacked LFO sweep limits (Converge to Notches, Sweep to Air, or Split Spectrum) ensuring zero frequency collision across engines.
* 🎙 **Studio-Grade Export:** Record your live modulated audio directly in the browser and export it to Uncompressed WAV or FLAC formats.
* 📊 **Holographic Visualizer Dashboard:** Real-time dual-canvas rendering featuring a Time-Domain / Phase Oscilloscope and an FFT Spectral Distribution analyzer.

---

## 🛠️ Installation & Usage

Because this application relies on standard browser Microphone security protocols (`getUserMedia`), it **cannot** be run directly from a `file://` URL. It must be hosted on a local or remote web server.

### Option 1: VS Code Live Server (Recommended)
1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/auraphaser.git
   ```
2. Open the folder in VS Code.
3. Install the **Live Server** extension.
4. Right-click `index.html` and select **"Open with Live Server"**.

### Option 2: Python HTTP Server
1. Clone the repository and navigate to the folder in your terminal.
2. Run a local python server:
   ```bash
   python -m http.server 8000
   ```
3. Open your browser and navigate to `http://localhost:8000`.

---

## 🗺️ Roadmap

The current version of AuraPhaser pushes vanilla JavaScript to its absolute limit. Future updates are planned to expand modulation parameters and spatial width.

- [ ] **WebMIDI Integration:** Map physical MIDI controllers to the Engine Spread, LFO Time, and Inversion triggers.
- [ ] **Offline File Processing:** Add a drag-and-drop feature to process pre-recorded audio files instead of relying purely on a live microphone.
- [ ] **HRTF 3D Spatialization:** Introduce an integer-based panning matrix to push specific phase-bands to hard-left/hard-right stereo fields.
- [ ] **Feedback Routing:** Allow output signals to route back into the APF inputs for extreme self-resonating comb-filter effects.
- [ ] **WebAssembly (WASM) / Rust Port:** Rewrite the `AudioWorkletProcessor` entirely in Rust via WASM for a theoretical 2x - 3x performance boost on massive track counts.

---

## 🛡️ License

This project is licensed under the MIT License. See the `LICENSE` file for details. 

*Disclaimer: Be mindful of your speaker volume when pushing track counts above 5,000. While the software utilizes mathematical root-mean-square normalization to prevent clipping, extreme phase summations can produce unpredictable resonant spikes.*
