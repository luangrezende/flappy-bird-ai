# Neuro-Bird

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.7+-red?logo=pytorch&logoColor=white)
![CUDA](https://img.shields.io/badge/CUDA-11.8+-green?logo=nvidia&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.12+-blue?logo=opencv&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?logo=windows&logoColor=white)
![GPU Required](https://img.shields.io/badge/GPU-Required-critical?logo=nvidia&logoColor=white)

An experimental **AI-driven Flappy Bird agent** built around **computer vision** and **neuroevolution**.  
The project focuses on **real-time perception**, **GPU-only processing**, and a **fully parameterized architecture** designed for performance, clarity, and controlled experimentation.

> **GPU required**: NVIDIA GPU with CUDA support. CPU execution is not supported.

---

## Overview

Neuro-Bird is designed to interact with a custom Flappy Bird executable and autonomously learn gameplay behavior using visual input only.

Core goals:
- Treat the game as a black box (no internal game state access)
- Rely exclusively on screen capture and vision-based perception
- Keep all system behavior configurable (no hardcoded parameters)
- Prioritize determinism, performance, and observability

The project is intentionally modular to support incremental evolution of the agent while keeping the perception layer stable and testable.

---

## Current Capabilities

### Implemented
- High-performance screen capture using MSS
- GPU-accelerated OCR score detection (EasyOCR)
- Vision preprocessing and region detection with OpenCV
- Fully externalized configuration via YAML
- Visual diagnostics separated from core logic
- Performance-oriented architecture (GPU-only path)

### In Progress
- NEAT-based neuroevolution engine
- Environment interaction and input simulation
- Population training and evaluation loops
- Model persistence and replay

---

## Game Dependency

This project requires a **specific Flappy Bird executable** developed to support reliable visual detection.

Download:
https://github.com/luangrezende/flappy-bird-python/releases

The perception system is calibrated for this version only. Other implementations are not supported.

---

## Project Structure

```
neuro-bird/
├── main.py                 # Entry point (training / execution)
├── config.yaml             # Centralized configuration (no hardcoded values)
├── requirements.txt
│
├── modules/
│   ├── vision/             # Vision and OCR logic (pure processing)
│   ├── agent/              # Neuroevolution and neural networks
│   ├── env/                # Game interaction layer
│   ├── training/           # Training loops and evaluation
│   └── utils/              # Shared utilities and config management
│
├── tests/
│   ├── test_score_detector.py
│   └── visual_renderer.py  # Isolated visualization utilities
│
└── assets/                 # Screenshots, recordings, saved models
```

---

## Configuration Model

All runtime behavior is driven by `config.yaml`.

Design principles:
- Zero magic numbers
- No conditional behavior based on code edits
- All thresholds, regions, and tuning parameters externally defined

Configurable domains include:
- Screen capture regions and FPS targets
- OCR thresholds and scaling
- Detection region positioning
- Agent evolution parameters
- Rendering diagnostics
- GPU and performance tuning

### Example

```yaml
vision:
  screen_capture:
    region: { top: 275, left: 520, width: 400, height: 700 }
    fps_target: 60

  ocr:
    gpu: true
    confidence_threshold: 0.3
    scale_factor: 3

agent:
  neat:
    population_size: 100
    max_generations: 200
```

---

## Architecture Notes

### Vision Pipeline
1. GPU-backed screen capture (MSS)
2. Configurable preprocessing and scaling
3. GPU OCR via EasyOCR
4. Region-based score detection
5. Optional visual overlays (isolated module)

### Design Decisions
- Vision logic is isolated from rendering
- Rendering is optional and non-blocking
- Configuration is loaded once via singleton
- CPU paths are intentionally excluded
- All modules favor explicit data flow over callbacks

---

## Installation

### Requirements
- Windows 10/11
- Python 3.8+
- NVIDIA GPU with CUDA support
- CUDA Toolkit 11.8+ (or compatible)
- Updated NVIDIA drivers

### Setup

```bash
git clone https://github.com/luangrezende/neuro-bird.git
cd neuro-bird
pip install -r requirements.txt
```

Verify CUDA availability:
```bash
nvidia-smi
```

---

## Usage

### Vision System Test

```bash
python tests/test_score_detector.py
```

This validates:
- Region positioning
- OCR accuracy
- GPU execution path
- Real-time performance metrics

All visualization parameters are controlled via `config.yaml`.

---

## Performance Characteristics

- Real-time processing at 60+ FPS (hardware-dependent)
- GPU-only execution path
- Minimal CPU utilization
- Configurable detection regions to control processing cost
- Deterministic behavior given fixed configuration

---

## Scope and Intent

This project is not intended as:
- A generic game bot framework
- A plug-and-play reinforcement learning toolkit
- A production-ready AI system

It is intended as:
- A controlled experiment in vision-based agents
- A reference for GPU-first real-time perception
- A foundation for evolutionary learning research

---

## License

MIT License.
